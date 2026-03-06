# How to Scrape a Small Social Media Platform

Reverse-engineering an API on deadline.

**NICAR 2026 | Jack Gillum and Brian Whitton, The Wall Street Journal**

## What this is

A hands-on workshop for scraping [Pilled.net](https://pilled.net), a small social media platform popular among conspiracy theorists. Unlike Twitter or Facebook, it's small enough to scrape entirely (~1 million posts) and has minimal anti-scraping measures, making it a good teaching example.

The scenario: your editor asks, *"A far-right group has been in the news. What have they been saying online?"* We go from that question to a cleaned dataset in Google Sheets.

## What you'll learn

1. **Everything on the page is a network call** — modern web apps load content via background API calls that return JSON. If you can see the call in DevTools, you can replay it.
2. **Reverse-engineer an API** using Chrome DevTools (Network tab, Fetch/XHR filter, Copy as cURL).
3. **Build a scraper in Python** — translate a cURL command into `requests.get()`, paginate, and save raw JSON.
4. **Clean and analyze the data** — filter, flatten, export to TSV, and answer basic questions (when are they posting? who are they boosting? how much reach?).

## Setup

### Software you need

- **Chrome** (for DevTools)
- **VS Code** with Jupyter notebook support
- **[uv](https://docs.astral.sh/uv/)** (Python package manager)

### Install dependencies

```bash
uv init pilled-scraper
cd pilled-scraper
uv venv
source .venv/bin/activate

uv pip install requests pandas jupyter ipykernel
uv pip install yt-dlp  # optional, for downloading media

uv run python -m ipykernel install --user --name pilled-scraper
```

## Workshop notebook

Open `scraping_pilled.ipynb` in VS Code and follow along. The notebook walks through:

| Section | What you do |
|---|---|
| Part 1 | Use DevTools to find the API endpoint behind a profile page |
| Part 2 | Translate the browser request into Python (`requests.get()`) |
| Part 3 | Paginate through all posts and save raw JSON |
| Part 4 | Clean the data into a DataFrame, export TSV for Google Sheets |
| Part 5 | Analyze posting activity, engagement, and sharing patterns |
| Bonus | Download video/media for archiving |

## What to look for in DevTools

| What | Where to find it |
|---|---|
| API endpoint URL | Network tab > Request URL |
| Pagination params | Query params: `page`, `offset`, `cursor`, `pageSize` |
| Outgoing headers | Headers tab: `Authorization`, `Cookie`, `Origin`, `Referer` |
| Rate limiting | Response headers: `X-RateLimit-*`, `Retry-After` |
| Response shape | Response body: array vs. object, `totalCount`, `hasMore` |
| Other clues | Error messages, API versioning, CORS headers |

## The general pattern

```
Browse site > DevTools Network > Find the call >
Copy as cURL > Test in terminal > Python requests >
Paginate > Save raw JSON > Clean DataFrame >
Export TSV > Google Sheets > Write the story
```

## Do's and Don'ts

**Do:**
- Rate-limit your requests (2-second delays between pages)
- Save raw data and methodology notes
- Archive with screenshots and/or the Wayback Machine
- Have a chat with your bosses about what you're doing

**Don't:**
- Hammer their server
- Bypass authentication for private data

## Continue learning

- [Chrome DevTools Network panel docs](https://developer.chrome.com/docs/devtools/network) — the official reference for everything we used in Part 1
- [Python `requests` library](https://docs.python-requests.org/) — the HTTP library we used to replay API calls
- [pandas documentation](https://pandas.pydata.org/docs/) — for cleaning and analyzing the data once you have it
- [uv](https://docs.astral.sh/uv/) — the Python package manager used in this workshop
- [yt-dlp](https://github.com/yt-dlp/yt-dlp) — for downloading video/media from many platforms

## Contact

Jack Gillum and Brian Whitton, The Wall Street Journal
