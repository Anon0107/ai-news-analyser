# ai-news-analyzer

CLI tool that fetches top Hacker News stories and generates AI-powered analysis using Claude — sentiment, key themes, importance scoring, and one-line summaries.

## What It Does

1. Fetches the top 10 stories from the Hacker News API
2. Sends each story to Claude (Haiku) for structured JSON analysis
3. Sorts results by importance score
4. Prints a formatted daily brief to the terminal

## Architecture

```
Hacker News API → fetch top 10 IDs → fetch story details → Claude analysis → formatted output
```

## Example Output

```
Input tokens: 2317, Output tokens: 803, Estimated cost: $0.006332.
TOP 10 LATEST NEWS (2026/04/02 14:33:12):
1 ) Live: Artemis II Launch Day Updates (positive)
   Summary         : NASA's Artemis II mission launch day updates provide real-time coverage of a major milestone in lunar exploration.
   Importance score: 9
   Themes          : space exploration, NASA missions, Artemis program, launch event
   URL             : https://www.nasa.gov/blogs/missions/2026/04/01/live-artemis-ii-launch-day-updates/
...
```

## Setup

**1. Clone the repo**
```bash
git clone https://github.com/Anon0107/ai-news-analyzer.git
cd ai-news-analyzer
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Configure environment**
```bash
cp .env.example .env
# Add your Anthropic API key to .env
```

**4. Run**
```bash
python ai_news_analyzer.py
```

## Requirements

- Python 3.11+
- Anthropic API key

## Key Concepts

- **Structured outputs** — Claude returns strict JSON via assistant prefill technique
- **Retry logic** — rate limit, server, and connection errors handled with up to 3 retries
- **Token tracking** — input/output tokens and estimated cost printed after every run
- **Graceful degradation** — stories that fail analysis are skipped, rest of run continues

## Cost

Using `claude-haiku-4-5`. Around **$0.004-0.007 per run** (10 stories, ~2-3k input tokens, ~500-1000 output tokens).