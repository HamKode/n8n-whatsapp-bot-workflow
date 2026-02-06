# n8n WhatsApp Bot Workflow

## Description
This n8n workflow automates WhatsApp messaging:
- Receive incoming messages via Twilio WhatsApp or other WhatsApp API
- Send automated responses based on workflow rules
- Log all messages and conversations to a database or Google Sheets
- Optional: Trigger notifications via email or Slack

## How to Use
1. Download the JSON file: `whatsapp-bot-workflow.json`
2. Open n8n
3. Click **Import Workflow**
4. [Import into n8n](https://n8n.io/workflows/import)
5. Upload the JSON file
6. Configure your credentials:
   - WhatsApp API (e.g., Twilio)
   - Email / Slack (optional)
   - Database (optional)
7. Activate the workflow

## Requirements
- n8n v1.x or higher
- Twilio / WhatsApp API credentials
- Optional: Database or Google Sheets for logging
- Optional: Email / Slack for notifications

## Author
Hussain Ahmed Madni

## License
MIT (or your choice)
