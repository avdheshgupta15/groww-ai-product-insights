# Groww AI Product Insights Workflow

## Project Overview

This project is an AI-powered Product + Support workflow that transforms raw customer reviews into structured product insights and ready-to-use customer communication.

The workflow analyzes recent Groww user reviews, identifies recurring product themes, detects a recurring fee/charge-related confusion, generates a weekly internal Product Pulse and a customer-facing Fee Explainer, and then uses a human approval gate before taking any external action.

After approval, the workflow:

- Appends the approved output to Google Docs
- Creates a Gmail draft
- Does not auto-send the email

The workflow is built in **n8n**.

---

## Problem Statement

Build an AI workflow that transforms raw customer feedback into:

1. Structured internal product insights
2. A weekly product update
3. A standardized customer-facing explanation for a recurring fee or charge

The workflow must include a human approval step before logging or sharing the generated content through external tools.

---

## Product Selected

**Groww**

Groww was selected because public customer reviews contain recurring feedback around:

- App performance
- Redemption and withdrawal delays
- Trade execution issues
- Customer support
- Fee and charge confusion

---

## Input Dataset

The workflow uses a CSV containing **31 public Groww reviews** collected from public review sources.

### CSV fields

\`\`\`text
review_id
review_date
rating
review_text
source
product
\`\`\`

The reviews are processed by the workflow and converted into a single structured input for AI analysis.

---

## Workflow Architecture

\`\`\`text
Reviews CSV
    ↓
Read Reviews CSV
    ↓
Extract Reviews
    ↓
Prepare Reviews
    ↓
Review Intelligence
    ↓
    ├───────────────┐
    ↓               ↓
Weekly Product   Fee Explainer
Pulse
    ↓               ↓
Format Weekly    Format Fee
Pulse       Explainer
    ↓               ↓
    └───────┬───────┘
           ↓
      Merge Outputs
           ↓
     Human Approval
           ↓
     Approval Check
           ↓
    ├──────────────┐
  True           False
    ↓               ↓
Google Docs     Stop Process
    ↓
Gmail Draft
\`\`\`

---

## Setup Instructions

1. **n8n Installation**: Install n8n (self-hosted or cloud).
2. **Import Workflow**: Import the JSON file located in the `workflow/` directory.
3. **Credentials**: Configure the following credentials in n8n:
   - Google Docs API
   - Gmail API
4. **Data Input**: Ensure `reviews.csv` is accessible to the n8n workflow.
5. **Test**: Run the workflow and check your email for the approval request.
