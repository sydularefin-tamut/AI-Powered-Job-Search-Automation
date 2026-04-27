# AI-Powered Job Search Automation

Automated daily job search workflow built with n8n, Claude AI, and JSearch API.

Searches 5 job categories every morning, filters matches using AI, saves results to Google Sheets, and sends email notifications — fully automated.

---

## What it does

- Runs every day at 10:00 AM automatically
- Searches 5 job categories across Dallas TX and remote
- Filters each job using Claude AI against your skills and profile
- Saves every matched job to Google Sheets with fit score and reason
- Emails you matched jobs with direct apply links

---

## Workflow Structure

```
Schedule Trigger (10am daily)
        ↓
5x HTTP Request nodes (JSearch API)
   - Financial Analyst Dallas TX
   - Staff Accountant Dallas TX
   - FPA Analyst remote
   - Accounting Analyst Dallas TX
   - AML Compliance Analyst remote
        ↓
Code node (extract and combine job data)
        ↓
Loop Over Items (process one job at a time)
        ↓
Claude AI (Message a model) — filter job
        ↓
Code node (parse AI verdict)
        ↓
IF node (verdict = true?)
   ↓                    ↓
Google Sheets        No Operation
(save match)         (discard)
   ↓
Gmail
(send email)
```

---

## Tools Used

| Tool | Purpose |
|---|---|
| n8n | Workflow automation |
| Claude AI (Anthropic) | AI job filtering |
| JSearch API via RapidAPI | Job data source |
| Google Sheets | Job match tracking |
| Gmail | Email notifications |

---

## Setup Instructions

### Step 1 — Get your API keys

- **RapidAPI key** — sign up free at rapidapi.com, subscribe to JSearch (free tier — 500 requests/month)
- **Anthropic API key** — sign up at console.anthropic.com, add $5 credit
- **Google account** — for Google Sheets and Gmail connections

### Step 2 — Import workflow into n8n

1. Sign up free at n8n.io
2. Create new workflow
3. Click 3 dots menu → Import from file
4. Upload the `workflow.json` file from this repository

### Step 3 — Add your credentials

Replace these placeholders in each node:

| Placeholder | Replace with |
|---|---|
| `YOUR_RAPIDAPI_KEY_HERE` | Your RapidAPI key |
| Connect Anthropic account | Your Anthropic API key |
| Connect Google Sheets | Your Google account |
| Connect Gmail | Your Google account |
| `YOUR_EMAIL_HERE` | Your email address |

### Step 4 — Set up Google Sheet

Create a Google Sheet with these column headers in Row 1:

```
verdict | fit | reason | jobTitle | company | location | jobUrl | date
```

### Step 5 — Customize your profile

In the **Message a model** node, update the candidate profile text to match your own skills and location.

### Step 6 — Activate

Click the Inactive toggle → turns Active → runs every day at 10am automatically.

---

## Cost

| Service | Free tier | Estimated usage |
|---|---|---|
| n8n | Free cloud plan | Within free limits |
| RapidAPI JSearch | 500 requests/month | ~150 requests/month |
| Anthropic Claude Haiku | Pay as you go | ~$1.50/month |
| Google Sheets | Free | Free |
| Gmail | Free | Free |

Total cost: approximately $1.50 per month.

---

## Customization

To change job search queries, update the URL in each HTTP Request node:

```
https://jsearch.p.rapidapi.com/search?query=YOUR+JOB+TITLE+HERE&page=1&num_pages=1&num_results=5
```

To change number of jobs per search, update `.slice(0, 2)` in Code in JavaScript node. Current setting: 2 jobs per search × 5 searches = 10 jobs per day.

---

## Author

Built by a finance professional to automate the job search process using AI.

**Skills:** Financial Analysis, GL Accounting, FPA, Budgeting, AML/CFT, CISA, MBA Finance, QuickBooks, Advanced Excel, Power BI

**Location:** Dallas, TX | Green Card Holder

---

## License

MIT License — free to use and modify.
