# /run-heatmaps

Set up or maintain local SEO heatmaps for a GBP location. Setup draws candidate keywords from existing work (rank tracker, research projects, organic rankings, prior heatmap config) and enriches them with volume/difficulty before you pick what to track. Maintenance reads the latest snapshot — SA dashboard handles weekly refresh, the toolkit does not duplicate it.

## Instructions

### Step 1: Choose Mode

Ask the user:
> Is this a **new heatmap setup** or **maintenance** (read latest snapshot + report deltas)?

### New Heatmap Setup

Load `workflows/heatmap-setup.yaml` and execute:

1. **Pre-flight: business + location** — `local_seo_heatmaps_list_businesses` (search by name or CID). If the business isn't linked, `local_seo_heatmaps_create_business` from the GBP location. **Halt if `Address: None`** — prompt the user to fix the location in the dashboard first. Grid accuracy depends on a real address.
2. **Quota check** — `local_seo_heatmaps_get_heatmap_quota`. Warn at <20% remaining, confirm before proceeding.
3. **Discover existing keyword work** (parallel pulls):
   - `local_seo_heatmaps_list_businesses_heatmaps` — existing tracking on this business
   - `krt_list_projects` for the domain + `krt_get_keywords_details` for each match
   - `se_list_keyword_research_projects` for the domain + `se_get_keyword_research_details`
   - `se_get_organic_keywords` — top 30–50 keywords the site already ranks for
4. **AI fallback (only if pool <15)** — `local_seo_heatmaps_recommend_keywords`. Flag suggestions explicitly as gemini-generated and warn: AI often misses the actual specialty (e.g., reads a roofer as a generic contractor). User should treat as inspiration, not truth.
5. **De-dupe + enrich** — `se_lookup_keyword` on the combined unique set for volume + difficulty + intent. Cache results.
6. **Present ranked candidate pool** — single table sorted by relevance score (volume × binary local-intent flag), grouped by provenance:
   - ✅ Already tracked (existing heatmap)
   - 📈 Already ranking (organic, with current position)
   - 🔍 From research (KRT / research project)
   - 💡 AI suggestion (gemini — use with caution)

   Each row: keyword · volume · difficulty · intent · source.
7. **User picks final tracking set** — recommend 10–15. Hard cap at 25 (quota burns fast above that).
8. **Manual-add prompt** — "Anything missing that you know is relevant?" Common reason: AI/research both miss the actual specialty.
9. **Grid preview** — `local_seo_heatmaps_preview_setup_heatmap` with final keywords + grid size (default 7×7) + radius (default 5mi). Show preview, confirm with user.
10. **Setup** — `local_seo_heatmaps_setup_heatmap`. Done. SA dashboard's weekly cron handles ongoing refresh.

Ask the user for: GBP location ID or business name, grid size (default 7×7), radius (default 5mi), which candidate keywords to track from the presented pool.

### Maintenance

Load `workflows/heatmap-maintenance.yaml` and execute:

1. **List heatmaps** — `local_seo_heatmaps_list_businesses_heatmaps` for the business.
2. **Latest snapshot** — `local_seo_heatmaps_get_heatmap_details` for the current snapshot.
3. **Per-keyword rank** — `local_seo_heatmaps_get_rank` for tracked keywords.
4. **Snapshot diff** — `local_seo_heatmaps_list_available_snapshot_dates` → diff current vs prior. Compute avg rank delta + visibility change + top movers.
5. **(Optional) Off-cycle refresh** — only if the user explicitly requests one (post-rebrand, new services, freshly fixed GBP issue). Otherwise the dashboard's weekly cron is the source of truth — do NOT refresh from the toolkit on a schedule.
6. **(Optional) Competitor comparison** — `local_seo_heatmaps_single_competitor_versus_report` for 1–2 competitors if the user asks. Opt-in, not default.

## Output Format

**Setup:**
```
✅ {business_name} — Heatmap Setup

📍 Business        linked (id: {business_id})                  View →
🔎 Discovered      {N} from existing · {N} KRT · {N} organic · {N} AI
🔑 Keywords        {N} tracked                                 View →
🗺️ Grid            {size} · {radius}mi · {points} points        View →
📊 Baseline        captured · avg rank {X}                     View →
🎫 Quota           {used}/{total} ({remaining} left)
```

**Maintenance:**
```
✅ {business_name} — Heatmap Snapshot · {period}

🗺️ Grid            {N} points · {keyword_count} keywords        View →
📈 Avg rank        {current} ({±Δ} vs last snapshot)            View →
🏆 Top movers      {keyword} ↑{N}, {keyword} ↓{N}               View →
🥊 Competitor      {name} avg rank {X} (you: {Y})               View →   ← if requested
🎫 Quota           {used}/{total} ({remaining} left)
```

## Golden Rules

- ALWAYS `preview_setup_heatmap` before `setup_heatmap` — grid spend is non-trivial
- Check `get_heatmap_quota` before any refresh; warn at <20% remaining
- Default grid: 7×7, 5mi radius. Larger burns quota fast — confirm before going bigger
- Don't refresh from the toolkit on a schedule — SA dashboard's weekly cron is the source of truth. Manual refresh is for off-cycle events only
- Keyword choice matters more than grid size — bias toward 10–15 sharp keywords over 30 mediocre ones
- Competitor reports are opt-in; don't run unprompted
- Per Golden Rule 1: schema-discover any tool called for the first time with `{}` before relying on it
