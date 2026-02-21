# GitHub Actions Free Tier: What You Can Actually Build

**What you get free:** 2,000 compute minutes per month on public repos. Unlimited on public repos (the limit is for private repos).

**What this means:** You can run automated workflows every day, multiple times a day, indefinitely, for $0.

---

## What the SolarPunk Mycelium Does on Free Tier

- Runs 10 scheduled workflows daily
- Sends emails automatically
- Generates and commits files
- Checks gallery health
- Reads and responds to emails
- Archives pages to the Internet Archive
- Updates living documentation with real stats
- Generates and publishes articles

All on the free tier. All public repos. Zero monthly cost.

---

## Workflow Basics

```yaml
# .github/workflows/my-workflow.yml
name: My Automated Task
on:
  schedule:
    - cron: '0 14 * * *'  # Every day at 2pm UTC
  workflow_dispatch:       # Also triggerable manually

jobs:
  run:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.11'
      - name: Do the thing
        run: python my_script.py
      - name: Save results
        run: |
          git config user.email "bot@example.com"
          git config user.name "Bot"
          git add . || true
          git diff --staged --quiet || git commit -m "auto: results"
          git push || true
```

## Cron Schedule Quick Reference

| Cron | When |
|------|------|
| `0 14 * * *` | Daily at 2pm UTC |
| `0 2 * * *` | Daily at 2am UTC |
| `0 10 * * 0` | Every Sunday at 10am UTC |
| `0 */6 * * *` | Every 6 hours |
| `*/30 * * * *` | Every 30 minutes |

## Secrets Management

Store API keys and passwords as GitHub Secrets (repo Settings → Secrets → Actions). They're encrypted and never visible in logs.

```yaml
- name: Run with secret
  env:
    MY_API_KEY: ${{ secrets.MY_API_KEY }}
  run: python script.py
```

## Committing Back to Repo from a Workflow

```yaml
- name: Commit results
  run: |
    git config user.email "action@github.com"
    git config user.name "GitHub Action"
    git add data/ results/ || true
    git diff --staged --quiet || git commit -m "auto: update"
    git push || true
```

---

## Real Things Built on Free Tier

- The entire SolarPunk Mycelium (10 workflows, email, AI generation)
- Automated PDF generation from markdown
- GitHub Pages sites with auto-updating stats
- Nightly data scraping and storage
- Automated social media posting (Mastodon, Discord webhooks)
- Email response systems

---

**Fork the Mycelium:** [github.com/meekotharaccoon-cell](https://github.com/meekotharaccoon-cell)
