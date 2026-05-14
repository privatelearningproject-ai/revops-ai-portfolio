# 🗣️ Jawab — AI Review Responder
**Paste a G2/Capterra review → get a professional, empathetic reply in seconds**

> Built for SaaS Customer Success teams. Runs locally via Llama3 + Ollama. No API key needed.

---

## The Problem

Every SaaS company gets reviewed on G2, Capterra, and Trustpilot. Responding to reviews — especially negative ones — is time-consuming, emotionally draining, and easy to get wrong. A defensive reply on a 2-star review can do more damage than the review itself.

**Jawab** (Arabic/Urdu for *"reply"*) handles the first draft. CS teams review, personalise, and post.

---

## Demo

```
═══════════════════════════════════════════════════════════
  🗣️  JAWAB — AI Review Responder
  Powered by Llama3 via Ollama
═══════════════════════════════════════════════════════════

Paste the customer review below.
When done, press Enter twice:

> The onboarding was confusing and support took 3 days to
> respond. The product itself is great once you figure it
> out but getting started was really frustrating.

⏳  Generating reply...

──────────────────────────────────────────────────────────
  JAWAB ANALYSIS
──────────────────────────────────────────────────────────
  SENTIMENT: Mixed
  RATING GUESS: 3 stars

  REPLY:
    Thank you for taking the time to share this — and
    we're really sorry the onboarding experience didn't
    match the product itself. A 3-day support response
    time is not acceptable, and we're actively working
    to fix that. We'd love to personally walk you
    through the setup so you can get the most out of
    the platform — please reach out to us at
    support@yourproduct.com and mention this review.
──────────────────────────────────────────────────────────
```

---

## How It Works

1. You paste a customer review into the terminal
2. Jawab sends it to **Llama3** running locally via **Ollama**
3. The model detects sentiment, guesses star rating, and drafts a reply
4. You copy, tweak, and post

No data leaves your machine. No API costs. Runs offline.

---

## Stack

| Tool | Role |
|------|------|
| Python | Core scripting |
| Ollama | Local LLM runtime |
| Llama3 | Language model (review analysis + reply generation) |

---

## Setup

**1. Install Ollama**
```bash
# Mac
brew install ollama

# Or download from https://ollama.com
```

**2. Pull Llama3**
```bash
ollama pull llama3
```

**3. Install Python dependency**
```bash
pip install ollama
```

**4. Run Jawab**
```bash
python jawab.py
```

---

## Customise for Your Product

Open `jawab.py` and update two lines:

```python
PRODUCT_NAME = "YourProduct"   # e.g. "Freshdesk"
COMPANY_NAME = "YourCompany"   # e.g. "Freshworks"
```

The system prompt automatically adapts.

---

## Why This Matters for RevOps

Review management is an underrated revenue lever:
- **G2 reviews influence 70%+ of B2B software purchases**
- A well-handled negative review can convert skeptics
- CS teams spend hours per week on this — Jawab cuts it to minutes

In a RevOps context, this slots into the **post-sale retention loop** — the same loop that lead scoring and sales call analysis feed into.

---

## Status

✅ Demo — working locally on Mac  
✅ Tested with positive, negative, and mixed reviews  
🔜 Planned: batch mode (CSV of reviews → bulk replies)  

---

## Related Projects

- [Lead Scoring Engine](../lead-scoring/) — AI qualification at the top of the funnel
- [Agency Trawler](../agency-trawler/) — Outbound lead generation across 9 countries
- [PitchPulse](../pitchpulse/) — AI analysis of sales calls
