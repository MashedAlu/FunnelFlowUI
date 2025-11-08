# Funnel Copywriter - AI Marketing Content Generator

## Overview
A web application that connects to n8n AI agents to generate comprehensive marketing content including market research, email sequences, and sales pages. Users fill out a detailed form about their business and funnel strategy, which is then processed by three specialized AI agents that stream responses back in real-time.

## Project Structure

### Frontend
- **Framework**: React with TypeScript, Vite
- **Styling**: Tailwind CSS with custom dark theme
- **UI Components**: Shadcn/ui components
- **Forms**: React Hook Form with Zod validation
- **Markdown Rendering**: react-markdown for displaying AI-generated content
- **Routing**: Wouter for client-side routing

### Backend
- **Framework**: Express.js
- **Purpose**: Proxy layer between frontend and n8n webhooks with streaming support
- **Routes**: Three POST endpoints for each content type
- **Features**: 
  - Environment validation at startup
  - Backpressure handling for long-running streams
  - Graceful cleanup on client disconnection
  - Detailed error messages with webhook status

### Key Features
1. **Multi-step Form**: Collects 13 business inputs with scrollable interface
2. **Three AI Agents**:
   - Market Research Agent (webhook: cb7f1e13-2985-4045-a98c-1f2d327299a8)
   - Email Sequence Agent (webhook: c5c70d5e-9d36-4daa-8536-e002d29bf8f1)
   - Sales Page Agent (webhook: 9b68b053-a43d-4977-a11b-c4d470ac7bc3)
3. **Streaming Responses**: Real-time display of AI-generated content as it's being created
4. **Tabbed Output**: Separate panels for each content type with markdown formatting
5. **Parallel Generation**: All three agents run simultaneously for faster results
6. **Partial Success Handling**: Shows results even if some generators fail

## Configuration

### Required Environment Variable
You **must** set the `N8N_WEBHOOK_URL` environment variable to your n8n instance base URL:

```bash
N8N_WEBHOOK_URL=https://your-n8n-instance.com/webhook
```

**Important**: Do not include the specific webhook IDs in this URL. The application will automatically append them.

### Setting Environment Variables in Replit
1. Click on "Tools" in the left sidebar
2. Select "Secrets"
3. Add a new secret:
   - Key: `N8N_WEBHOOK_URL`
   - Value: Your n8n webhook base URL (e.g., `https://your-n8n-instance.com/webhook`)

### Validation
The application validates the webhook URL at startup. If not configured, you'll see a warning in the console:
```
⚠️  N8N_WEBHOOK_URL is not configured properly. Please set it to your n8n instance base URL.
   Example: N8N_WEBHOOK_URL=https://your-n8n-instance.com/webhook
```

## Form Fields
All fields are required except "Existing Copy Sample":

1. **Funnel Strategy (paste here)** - Large textarea for comprehensive strategy document
2. **Business/Product Name** - Your business or product name
3. **Industry/Business Type** - e.g., SaaS, E-commerce, Coaching
4. **Target Audience (Be Specific)** - Detailed description of ideal customer
5. **Primary Funnel Type** - e.g., Webinar, VSL, Lead Magnet
6. **Conversion Goal & Current Performance** - Current metrics and targets
7. **Brand Voice & Personality** - e.g., Professional, Friendly, Bold
8. **Top 3 Product Benefits** - Key benefits your product provides
9. **Top 3 Pain Points You Solve** - Main problems you address
10. **Unique Value Proposition** - What makes you different
11. **Special Offers/Urgency Elements** - Limited time offers, bonuses, etc.
12. **Existing Copy Sample (Optional)** - Reference material for AI agents
13. **Success Metrics to Track** - KPIs like conversion rate, email open rate

## API Routes

### POST /api/generate/market-research
Generates comprehensive market research based on form data.
- **Webhook**: cb7f1e13-2985-4045-a98c-1f2d327299a8
- **Response**: Streaming text/event-stream
- **Errors**:
  - `503`: N8N webhook not configured
  - `500`: Internal server error or webhook unavailable
  - Webhook status codes: Passed through from n8n

### POST /api/generate/email-sequence
Generates value-dense email sequence.
- **Webhook**: c5c70d5e-9d36-4daa-8536-e002d29bf8f1
- **Response**: Streaming text/event-stream
- **Errors**: Same as above

### POST /api/generate/sales-page
Generates high-converting sales page copy.
- **Webhook**: 9b68b053-a43d-4977-a11b-c4d470ac7bc3
- **Response**: Streaming text/event-stream
- **Errors**: Same as above

All routes:
- Accept full form data as JSON in request body
- Return streaming responses (text/event-stream)
- Handle backpressure properly for long-running streams
- Clean up gracefully on client disconnection
- Provide detailed error messages on failure

## User Interface

### Layout
- **Two-column responsive layout**:
  - Left (40%): Scrollable form with all input fields
  - Right (60%): Tabbed output panels
- **Dark theme** with custom scrollbar styling
- **Professional typography** using Inter font
- **Mobile-responsive** - stacks vertically on smaller screens

### User Experience
1. User fills out the form (scrollable to access all fields)
2. Progress indicator shows "Step 1 of 2, 50% Complete"
3. Back button is available (currently disabled as it's step 1)
4. "Generate Research" button submits form
5. All three AI agents run in parallel
6. Content streams in real-time to respective tabs
7. Loading spinners show while generating
8. Success/error toasts notify of completion status
9. Partial success supported - shows results even if some generators fail

### Error Handling
- **Form validation**: Real-time validation with clear error messages
- **Network errors**: Toast notifications with specific error details
- **Partial failures**: Shows which generators failed and why
- **Webhook configuration**: Clear warning if N8N_WEBHOOK_URL not set
- **Loading states**: Always cleared on success or failure to prevent infinite spinning

## Development

### Running Locally
```bash
npm install
npm run dev
```

Server runs on port 5000 with both frontend and backend.

### Project Files
- `client/src/pages/Dashboard.tsx` - Main page with form and output panels
- `client/src/components/FunnelForm.tsx` - Form component with all fields
- `client/src/components/OutputPanel.tsx` - Output display with markdown rendering
- `server/routes.ts` - Backend proxy routes for n8n webhooks
- `shared/schema.ts` - Zod validation schema for form data
- `client/src/index.css` - Custom styles including dark scrollbar

### Testing
The application includes test IDs for automation:
- Form inputs: `input-{field-name-kebab-case}`
- Buttons: `button-back`, `button-generate`
- Tabs: `tab-market-research`, `tab-email-sequence`, `tab-sales-page`
- Page elements: `text-page-title`, output content elements

## Production Deployment

### Prerequisites
1. Set `N8N_WEBHOOK_URL` environment variable in production
2. Ensure n8n webhooks are accessible from your deployment
3. Verify CORS settings if n8n is on different domain

### Monitoring
Monitor these logs in production:
- Startup warning about N8N_WEBHOOK_URL configuration
- Webhook errors with specific failure reasons
- Streaming interruptions or backpressure issues

### Error Response Mapping
- **503 Service Unavailable**: N8N_WEBHOOK_URL not configured
- **500 Internal Server Error**: Webhook unreachable or stream error
- **4xx/5xx from webhook**: n8n agent error (check n8n logs)

## Troubleshooting

### "N8N webhook is not configured" error
- Set the `N8N_WEBHOOK_URL` environment variable
- Restart the application
- Verify the URL doesn't include "your-n8n-instance" placeholder

### Infinite loading spinners
- Check browser console for errors
- Verify n8n webhooks are responding
- Check network tab for streaming responses

### Content not displaying
- Verify markdown is being streamed from n8n
- Check that n8n agents are returning text content
- Look for errors in browser console

### Partial failures
- Check which specific webhook failed in the error toast
- Verify that specific n8n workflow is active
- Check n8n logs for agent-specific errors

## Recent Changes
- Added all 13 form fields with proper validation
- Implemented scrollable form container with dark theme scrollbar
- Added back button to form navigation
- Created backend proxy routes for n8n integration
- Implemented streaming response handling with backpressure support
- Added graceful cleanup on client disconnection
- Improved error handling with partial success notifications
- Added environment variable validation at startup
- Fixed loading state management to prevent infinite spinning
