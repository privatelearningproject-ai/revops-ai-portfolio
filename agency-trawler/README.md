# 🌐 Agency Trawler
**Multi-country lead generation engine — production tool, PublishStory**

> Scrapes Google in local languages across 9 countries. Generated 300+ agency leads, replacing manual research and third-party data spend (Lusha).

---

## The Problem It Solved

PublishStory needed a pipeline of digital agency leads across emerging markets. The old process: manual Google searches, one country at a time, ~5 leads per session. Expensive enrichment tools (Lusha) on top of that.

**Agency Trawler replaced all of it** — scripted, repeatable, multi-country, multilingual.

---

## What It Does

- Queries Google via **Serper API** using local-language search strings (e.g. "dijital ajans" in Turkish, "وكالة رقمية" in Arabic)
- Extracts agency names, websites, and contact signals from search results
- Deduplicates and structures output into a clean lead list
- Exports to **Google Drive** for direct sales team use
- Runs entirely on **Google Colab** — no local setup needed

---

## Countries Covered

| Region | Countries |
|--------|-----------|
| Middle East | UAE, Saudi Arabia, Qatar, Egypt |
| Southeast Asia | Indonesia, Malaysia |
| Africa | Nigeria |
| South Asia | India, Nepal |
| North America | USA |

---

## Results

| Metric | Before | After |
|--------|--------|-------|
| Leads per session | ~5 (manual) | 30–50 (automated) |
| Countries covered | 1 at a time | 9 simultaneously |
| Lusha / enrichment spend | Ongoing cost | Eliminated |
| Total leads generated | — | **300+** |

---

## Stack

| Tool | Role |
|------|------|
| Python | Core scripting |
| Serper API | Google search programmatic access |
| Pandas | Data cleaning + deduplication |
| Google Colab | Execution environment |
| Google Drive | Output + sharing with sales team |

---

## How It Works

```python
# Simplified core logic

queries = {
    "turkey": "dijital pazarlama ajansı",
    "egypt": "وكالة تسويق رقمي",
    "indonesia": "agensi pemasaran digital",
    "malaysia": "agensi digital Malaysia",
    "nigeria": "digital marketing agency Nigeria",
    "uae": "digital agency Dubai",
    "saudi": "شركة تسويق إلكتروني",
    "qatar": "digital agency Doha",
    "india": "digital marketing agency India",
}

for country, query in queries.items():
    results = serper_search(query)
    leads = extract_leads(results)
    all_leads.append(leads)

df = pd.DataFrame(all_leads).drop_duplicates(subset="website")
df.to_csv("agency_leads.csv")
```

---

## Why This Matters for RevOps

This is outbound prospecting infrastructure — the kind of tool that normally costs $$$ via ZoomInfo, Apollo, or Lusha. Built in-house, runs on demand, speaks the local language of each market.

For a company expanding into emerging markets, this is the difference between a 3-week research sprint and a 3-hour script run.

---

## Status

✅ Production — actively used at PublishStory  
✅ 300+ leads generated across 9 countries  
✅ Replaced manual research + third-party data tools  

---

## Related Projects

- [Lead Scoring Engine](../lead-scoring/) — AI qualification after leads enter the funnel
- [PitchPulse](../pitchpulse/) — AI analysis of sales calls after leads are engaged
