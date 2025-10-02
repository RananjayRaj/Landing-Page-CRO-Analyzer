# 🎯 Landing-Page-CRO-Analyzer
An AI-powered n8n workflow that analyzes landing pages and provides detailed Conversion Rate Optimization (CRO) recommendations using AI.

**📋 Overview
**
This workflow analyzes your landing pages and competitor pages to provide:

**Executive Summary** - Quick overview of key findings
**Issues & Challenges** - Identified problems impacting conversions
**Quick Wins **- Fast improvements you can implement in <30 minutes
**Detailed Recommendations** - Prioritized action items with expected impact
**Competitive Comparison **- How you stack up against competitors (optional)

**✨ Features**

**🤖 AI-Powered Analysis** using Claude Sonnet 4.5
**📊 Beautiful HTML Reports **sent directly to your email
**🔄 Competitor Comparison** - Analyze multiple pages simultaneously
**🎨 Professional Formatting** with priority badges and visual hierarchy
**⚡ Quick Wins** section for immediate actionable improvements
**🏆 Competitive Intelligence** showing advantages and opportunities

**🛠️ Prerequisites**

**1. n8n instance** (self-hosted or cloud)
**2. Anthropic API Key** (for Claude Sonnet 4.5)
**3. Gmail Account** with OAuth2 setup in n8n
**4. Jina.ai Reader **(free tier works fine - no API key required)

**📦 Quick Start**

1. Clone the repo and open your n8n instance
2. Import the workflow: **Import → From File** → Landing-Page-CRO-Analyzer-Sanitized.json
3. Create credentials in n8n (do NOT paste secrets into code nodes):

- Anthropic API credential
- Gmail OAuth2 credential


4. Attach credentials via the n8n UI to the corresponding nodes:

- Message a model → attach Anthropic credential
- Send Email Report → attach Gmail credential

5. Replace placeholders in node parameters within the n8n UI:

NOTIFICATION_EMAIL → recipient email for report

6. Activate the workflow
7. Copy the webhook URL and start analyzing landing pages!

**🚀 Usage
****Web Form Method
**
1. Navigate to the webhook URL provided by n8n
2. Enter your landing page URL
3. (Optional) Add competitor URLs separated by commas
4. Click Submit
5. Receive detailed CRO analysis via email within 60 seconds

API Method
bashcurl -X POST 'YOUR_N8N_WEBHOOK_URL' \
  -H 'Content-Type: application/json' \
  -d '{
    "Landing Page URL": "https://yoursite.com",
    "Competitor URLs (comma-separated)": "https://competitor1.com, https://competitor2.com"
  }'
**📊 Report Structure
**The generated report includes:

**1. Executive Summary** - High-level overview
**2. Issues & Challenges** - Problems to address
**3. Quick Wins** - Fast improvements (<30 min)
**4. Detailed Recommendations **- Prioritized by High/Medium/Low
**5. Competitive Comparison **(if competitors provided)

**🔧 Configuration
**
**- Email Recipients**: Set recipients
**- Report Styling**: Edit HTML template in "Format HTML Report" node

**🔐 Security Notes
**
- Never commit real API keys or credentials to the repository
- Store environment variables securely
- If a secret was committed accidentally, revoke/rotate it immediately

📝 Files

- Landing-Page-CRO-Analyzer-Sanitized.json - Sanitized n8n workflow (importable)
- .env.example - Example environment variables with placeholders
- README.md - This file
- Technical-Architecture.md - Detailed architecture documentation

**📧 Support
**For issues, questions, or suggestions:

- Check the n8n community forum
- Review Anthropic's documentation

**💡 Use Cases
**
- **Marketing Teams** - Optimize campaign landing pages
- **Product Managers** - Improve product pages
- **Agencies** - Deliver client audits automatically
- **E-commerce** - Enhance product and checkout pages
- **SaaS Companies** - Boost signup page conversions

📄 License
This project is licensed under the MIT License - see the LICENSE file for details.
