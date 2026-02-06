# WhatsApp AI Bot Complete Setup Guide

## Overview
This guide will help you set up a complete WhatsApp AI bot using n8n automation platform. The bot integrates with Google Gemini AI, Google Sheets for data management, and WhatsApp Business API for messaging.

## Prerequisites
- n8n automation platform (self-hosted or cloud)
- WhatsApp Business Account
- Google Cloud Platform account
- Google Sheets access
- Basic understanding of workflow automation

## Step 1: Install and Setup n8n

### Option A: Cloud Version (Recommended for beginners)
1. Visit [n8n.cloud](https://n8n.cloud)
2. Create an account and choose a plan
3. Access your n8n instance through the web interface

### Option B: Self-hosted Version
1. Install Node.js (version 16 or higher)
2. Install n8n globally:
   ```bash
   npm install n8n -g
   ```
3. Start n8n:
   ```bash
   n8n start
   ```
4. Access n8n at `http://localhost:5678`

## Step 2: Import the Workflow

1. Download the clean workflow file: `whatsapp bot - clean.json`
2. In n8n interface, click on "Import from File"
3. Select the downloaded JSON file
4. The workflow will be imported with all nodes

## Step 3: Configure WhatsApp Business API

### Setup WhatsApp Business Account
1. Go to [Facebook Business Manager](https://business.facebook.com)
2. Create a WhatsApp Business Account
3. Get your WhatsApp Business API credentials:
   - Phone Number ID
   - Access Token
   - Webhook Verify Token

### Configure WhatsApp Trigger Node
1. Click on "WhatsApp Trigger" node
2. Add WhatsApp credentials:
   - **Access Token**: Your WhatsApp Business API token
   - **Phone Number ID**: Your WhatsApp phone number ID
   - **Webhook Verify Token**: Create a secure random string
3. Set webhook URL in Facebook Developer Console to your n8n webhook URL

### Configure Send Message Node
1. Click on "Send message" node
2. Use the same WhatsApp credentials as the trigger
3. Configure message parameters as needed

## Step 4: Setup Google Gemini AI

### Get Google Gemini API Key
1. Visit [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Create a new API key
3. Copy the API key for later use

### Configure Google Gemini Chat Model Node
1. Click on "Google Gemini Chat Model" node
2. Create new credentials:
   - **Credential Name**: Give it a descriptive name
   - **API Key**: Paste your Google Gemini API key
3. Save the credentials
4. Configure model parameters:
   - **Model**: gemini-pro (recommended)
   - **Temperature**: 0.7 (for balanced creativity)
   - **Max Tokens**: 1000 (adjust as needed)

## Step 5: Setup Google Sheets Integration

### Enable Google Sheets API
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a new project or select existing one
3. Enable Google Sheets API
4. Create OAuth 2.0 credentials

### Configure Google Sheets Nodes
For each Google Sheets node (Post orders, Get FAQS, Get Inventory):

1. Click on the node
2. Create new Google Sheets credentials:
   - **Credential Type**: OAuth2
   - **Client ID**: From Google Cloud Console
   - **Client Secret**: From Google Cloud Console
   - **Scope**: https://www.googleapis.com/auth/spreadsheets
3. Authorize the connection
4. Configure sheet parameters:
   - **Document ID**: Your Google Sheet ID (from URL)
   - **Sheet Name**: Specific sheet tab name

### Prepare Your Google Sheets
Create three sheets with appropriate headers:

**Orders Sheet** (for Post orders node):
- Column A: Timestamp
- Column B: Customer Phone
- Column C: Order Details
- Column D: Status

**FAQs Sheet** (for Get FAQS node):
- Column A: Question
- Column B: Answer
- Column C: Category

**Inventory Sheet** (for Get Inventory node):
- Column A: Product Name
- Column B: Price
- Column C: Stock Quantity
- Column D: Description

## Step 6: Configure AI Agent

### Setup AI Agent Node
1. Click on "AI Agent" node
2. Configure agent parameters:
   - **Agent Type**: Conversational Agent
   - **System Message**: Define your bot's personality and instructions
   - **Max Iterations**: 5 (recommended)
   - **Memory**: Connect to Simple Memory node

### Example System Message:
```
You are a helpful customer service assistant for [Your Business Name]. 
You can help customers with:
- Product inquiries (check inventory)
- Frequently asked questions
- Order placement and tracking
- General support

Always be polite, professional, and helpful. If you cannot answer a question, 
politely ask the customer to contact human support.
```

## Step 7: Configure Memory System

### Simple Memory Node
1. Click on "Simple Memory" node
2. Configure memory settings:
   - **Memory Size**: 10 (number of previous messages to remember)
   - **Memory Type**: Buffer Window Memory

## Step 8: Test the Workflow

### Testing Steps
1. Save the workflow in n8n
2. Activate the workflow by clicking the toggle switch
3. Send a test message to your WhatsApp Business number
4. Check n8n execution log for any errors
5. Verify responses are working correctly

### Common Testing Scenarios
- Send "Hello" to test basic response
- Ask about products to test inventory integration
- Ask a FAQ to test knowledge base
- Try placing an order to test order processing

## Step 9: Deployment and Monitoring

### Production Deployment
1. Ensure all credentials are properly configured
2. Set up proper error handling
3. Configure webhook URLs for production
4. Test thoroughly before going live

### Monitoring
1. Monitor n8n execution logs regularly
2. Set up alerts for failed executions
3. Track response times and user satisfaction
4. Update FAQs and inventory regularly

## Troubleshooting

### Common Issues and Solutions

**WhatsApp Connection Issues:**
- Verify webhook URL is accessible
- Check access token validity
- Ensure phone number is verified

**Google Sheets Access Issues:**
- Verify OAuth credentials
- Check sheet permissions
- Ensure correct sheet IDs

**AI Response Issues:**
- Check Gemini API key validity
- Verify API quotas and limits
- Review system message configuration

**Memory Issues:**
- Clear memory if responses seem inconsistent
- Adjust memory window size
- Check memory node connections

## Security Best Practices

1. **Never share credentials** in workflow files
2. Use **environment variables** for sensitive data
3. **Regularly rotate** API keys and tokens
4. **Monitor usage** to detect unusual activity
5. **Implement rate limiting** to prevent abuse
6. **Use HTTPS** for all webhook URLs
7. **Validate input** to prevent injection attacks

## Maintenance

### Regular Tasks
- Update Google Sheets data weekly
- Review and update FAQs monthly
- Monitor API usage and costs
- Check for n8n updates
- Backup workflow configurations

### Performance Optimization
- Optimize Google Sheets queries
- Implement caching where possible
- Monitor response times
- Scale resources as needed

## Support and Resources

### Documentation Links
- [n8n Documentation](https://docs.n8n.io)
- [WhatsApp Business API](https://developers.facebook.com/docs/whatsapp)
- [Google Gemini API](https://ai.google.dev/docs)
- [Google Sheets API](https://developers.google.com/sheets/api)

### Community Support
- n8n Community Forum
- WhatsApp Business API Support
- Google AI Developer Community

---

**Setup Guide Created by: Hussain Ahmed Madni**

*This comprehensive guide ensures your WhatsApp AI bot is properly configured, secure, and ready for production use. Follow each step carefully and test thoroughly before deployment.*