# Funnel Copywriter

AI-powered marketing content generator that creates market research, email sequences, and sales pages using n8n AI agents.

## Quick Start

### 1. Configure n8n Webhook URL

Set your n8n webhook base URL as an environment variable:

```bash
N8N_WEBHOOK_URL=https://your-n8n-instance.com/webhook
```

**In Replit:**
1. Click "Tools" → "Secrets"
2. Add new secret: `N8N_WEBHOOK_URL` = `https://your-n8n-instance.com/webhook`

### 2. Run the Application

```bash
npm install
npm run dev
```

Visit http://localhost:5000 to access the application.

## How It Works

1. **Fill Out the Form** - Provide your business information, funnel strategy, and marketing details
2. **Generate Content** - Click "Generate Research" to run all three AI agents in parallel
3. **View Results** - Content streams in real-time to three separate tabs:
   - Market Research Output
   - Email Sequence Output
   - Sales Page Output

## Features

- ✅ **13-field comprehensive form** with validation
- ✅ **Real-time streaming** of AI-generated content
- ✅ **Parallel generation** - all agents run simultaneously
- ✅ **Markdown rendering** for beautiful formatted output
- ✅ **Dark theme** with custom scrollbars
- ✅ **Partial success handling** - see results even if some generators fail
- ✅ **Mobile responsive** design

## Required Form Fields

1. Funnel Strategy (paste here)
2. Business/Product Name
3. Industry/Business Type
4. Target Audience (Be Specific)
5. Primary Funnel Type
6. Conversion Goal & Current Performance
7. Brand Voice & Personality
8. Top 3 Product Benefits
9. Top 3 Pain Points You Solve
10. Unique Value Proposition
11. Special Offers/Urgency Elements
12. Existing Copy Sample (Optional)
13. Success Metrics to Track

## n8n Webhook Integration

This application connects to three n8n webhooks (configured in your n8n instance):

- **Market Research Agent** - `cb7f1e13-2985-4045-a98c-1f2d327299a8`
- **Email Sequence Agent** - `c5c70d5e-9d36-4daa-8536-e002d29bf8f1`
- **Sales Page Agent** - `9b68b053-a43d-4977-a11b-c4d470ac7bc3`

The backend automatically appends these IDs to your configured `N8N_WEBHOOK_URL`.

## Tech Stack

- **Frontend**: React, TypeScript, Tailwind CSS, Shadcn UI
- **Backend**: Express.js with streaming proxy
- **Validation**: Zod with React Hook Form
- **Markdown**: react-markdown

## Documentation

- API route details
- Error handling
- Production deployment
- Troubleshooting guide

