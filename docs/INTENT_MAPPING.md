# Intent → Tool Mapping Reference

> Quick reference card for mapping natural language intent to SearchAtlas MCP tools.
> Use this to route user requests to the correct workflow template.

---

## Keyword → Tool Table

| User says… | Primary Tools | Workflow Template |
|------------|--------------|-------------------|
| "audit", "site health", "issues", "crawl" | `audit_management`, `holistic_audit` | A or B |
| "new client", "onboard", "set up project" | `project_management`, full onboarding flow | **A — New Client SEO Onboarding** |
| "sync client", "push to brand vault", "pull from SA", "update brand profile", "brand vault out of date" | `brand_vault` (push/pull) | `/sync-client` |
| "monthly", "maintenance", "recurring SEO" | `suggestion_management`, `schema_markup` | **B — Monthly SEO Maintenance** |
| "brand vault", "brand voice", "brand profile", "brand" | `brand_vault` | A (step 4) |
| "topical map", "content strategy", "content plan", "content calendar" | `topical_maps` | A (step 6) or B (step 5) |
| "content", "blog", "article", "write", "generate article" | `topical_maps` → `content_generation` | A/B content steps |
| "content grader", "grade article", "optimize article" | `article_management` | B (step 7) |
| "publish", "WordPress", "CMS" | `content_publication` | B (step 7+) |
| "GBP optimization", "fix GBP profile", "Google Business" | `gbp_locations_recommendations`, `gbp_locations_categories_crud`, `gbp_locations_services_crud`, `gbp_locations_attributes_crud` | **C — GBP Profile Optimization** |
| "GBP posts", "post schedule", "social posts" | `gbp_posts_generation`, `gbp_posts_automation`, `gbp_posts_crud` | **D — GBP Monthly Recurring** |
| "reviews", "reply reviews", "review responses" | `gbp_reviews` | D (step 1) |
| "GBP stats", "GBP performance", "profile analytics" | `gbp_locations_crud` (op: `get_location_stats`) | D (step 5) |
| "PPC", "ads", "campaign", "Google Ads", "paid search" | `business_crud`, `product_crud`, `campaign` | **E — PPC Campaign Launch** |
| "landing page", "website", "web page" | `website_studio_tools` | E (step 7, optional) |
| "local SEO", "heatmap", "map pack", "local rankings", "geo grid", "set up heatmap", "track local rankings" | `local_seo_heatmaps_*` | **`/run-heatmaps`** (setup or maintenance) |
| "press release", "PR distribution" | `press_release_content`, `press_release_distribution` | **F — Authority Building** |
| "cloud stack", "cloud network" | `cloud_stack_content`, `cloud_stack_distribution` | F (steps 3–4) |
| "backlinks", "link building", "outreach", "digital PR" | `digital_pr_*`, `backlinks` | F (steps 5–6) |
| "LLM", "AI visibility", "ChatGPT mentions", "AI search" | `visibility`, `prompt_simulator` | **G — LLM Visibility & Reporting** |
| "sentiment", "brand sentiment" | `sentiment` | G (step 2) |
| "schema", "structured data", "schema markup" | `schema_markup` | B (step 3) |
| "indexing", "index now", "IndexNow", "sitemap" | `indexing_management` | B (step 4) |
| "keywords", "keyword research", "keyword list" | `keyword_research` | A (step 5) |
| "SERP", "rankings", "position distribution" | `analysis`, `organic` | G (step 4) |
| "report", "summary", "export", "Google Sheet" | `project_management` (op: `work_summary_export`) | G (step 5) |
| "SEO issues", "website issues", "recommendations" | `seo_analysis` | Standalone |

---

## Tool → Dashboard Link Patterns

| Tool | Dashboard URL Pattern |
|------|-----------------------|
| `project_management` | `https://dashboard.searchatlas.com/otto/` |
| `audit_management` | `https://dashboard.searchatlas.com/otto/site-audit/` |
| `brand_vault` | `https://dashboard.searchatlas.com/brand-vault/` |
| `topical_maps` | `https://dashboard.searchatlas.com/content/topical-maps/` |
| `content_generation` | `https://dashboard.searchatlas.com/content/articles/` |
| `article_management` | `https://dashboard.searchatlas.com/content/articles/` |
| `gbp_*` | `https://dashboard.searchatlas.com/gbp/` |
| `local_seo_*` | `https://dashboard.searchatlas.com/local-seo/` |
| `business_crud`, `product_crud`, `campaign` | `https://dashboard.searchatlas.com/otto-ppc/` |
| `press_release_*` | `https://dashboard.searchatlas.com/press-releases/` |
| `cloud_stack_*` | `https://dashboard.searchatlas.com/cloud-stacks/` |
| `digital_pr_*` | `https://dashboard.searchatlas.com/digital-pr/` |
| `visibility` | `https://dashboard.searchatlas.com/llm-visibility/` |
| `analysis`, `organic`, `backlinks` | `https://dashboard.searchatlas.com/site-explorer/` |
| `website_studio_tools` | `https://dashboard.searchatlas.com/website-studio/` |

---

## Deprecated Tools

| Deprecated | Replacement | Reason |
|-----------|-------------|--------|
| `OTTO_Knowledge_Graph` | `brand_vault` | All KG ops now in Brand Vault |
| `OTTO_Project_Management` | `project_management` | Renamed — same operations |
| `OTTO_Audit_Management` | `audit_management` | Renamed — same operations |
| `OTTO_Suggestion_Management` | `suggestion_management` | Renamed — same operations |
| `OTTO_Schema_Markup` | `schema_markup` | Renamed — same operations |
| `OTTO_Indexing_Management` | `indexing_management` | Renamed — same operations |
| `OTTO_Recrawl_Management` | `recrawl_management` | Renamed — same operations |
| `OTTO_Image_Upload` | `image_upload` | Renamed — same operations |
| `OTTO_Quota_Management` | `quota_management` | Renamed — same operations |
| `BrandVaultTools` | `brand_vault` | Renamed — same operations |
| `Site_Explorer_*` | `projects`, `organic`, `backlinks`, `analysis`, `adwords`, `keyword_research`, `brand_signals`, `holistic_audit` | Renamed — same operations |
| `Content_Generation_Tool` | `content_generation` | Renamed — same operations |
| `Article_Management_Tools` | `article_management` | Renamed — same operations |
| `Content_Retrieval_Tools` | `content_retrieval` | Renamed — same operations |
| `Content_Publication_Tools` | `content_publication` | Renamed — same operations |
| `Topical_Maps_Tools` | `topical_maps` | Renamed — same operations |
| `Visibility_Analysis_Tools` | `visibility` | Renamed — same operations |
| `Sentiment_Analysis_Tools` | `sentiment` | Renamed — same operations |
| `Query_Management_Tools` | `queries` | Renamed — same operations |
| `Prompt_Simulator_Tools` | `prompt_simulator` | Renamed — same operations |
| `otto_ppc_business_crud` | `business_crud` | Renamed — same operations |
| `otto_ppc_product_crud` | `product_crud` | Renamed — same operations |
| `otto_ppc_product_mgmt` | `product_mgmt` | Renamed — same operations |
| `otto_ppc_campaign` | `campaign` | Renamed — same operations |
| `otto_ppc_task` | `task` | Renamed — same operations |
| `otto_ppc_ads_account_crud` | `ads_account_crud` | Renamed — same operations |
| `otto_ppc_ads_account_mgmt` | `ads_account_mgmt` | Renamed — same operations |
| `gbp_stats` | `gbp_locations_crud` (op: `get_location_stats`) | Merged into gbp_locations_crud |

---

## Multi-Intent Routing

When user intent spans multiple tools, chain workflows in this priority order:

1. **Infrastructure first:** OTTO project, audit, indexing, schema
2. **Brand/content foundation:** Brand vault, topical map
3. **Content execution:** Article generation, grading, publishing
4. **Promotion:** Press release, cloud stack, digital PR
5. **Local/GBP:** GBP optimization, posts, reviews
6. **Paid:** PPC campaign setup
7. **Reporting:** LLM visibility, analytics, exports

---

## Ambiguous Intent Resolution

| Ambiguous phrase | Ask user | Possible routes |
|-----------------|----------|----------------|
| "content" | "Do you mean creating new articles or optimizing existing ones?" | New → topical_maps + content_generation / Existing → article_management |
| "set up GBP" | "Is this a first-time setup or monthly optimization?" | First time → C (full optimization) / Monthly → D (recurring) |
| "campaign" | "PPC ads campaign or digital PR outreach campaign?" | PPC → E / Outreach → F |
| "heatmap" | "New setup or just read the latest snapshot?" | New → `/run-heatmaps` setup / Read → `/run-heatmaps` maintenance (or `/run-gbp` monthly, which surfaces snapshot deltas as a side-effect) |
| "report" | "SEO summary report or LLM visibility report?" | SEO → project_management export / LLM → G |
| "issues" | "OTTO project issues or detailed SEO analysis?" | OTTO → project_management / Detailed → seo_analysis |
