# 🚀 Landing Page CRO Analyzer (n8n Workflow)

## Overview
This n8n workflow performs automated **Conversion Rate Optimization (CRO) analysis** of landing pages.  
It scrapes landing page content, passes it to an AI model (Anthropic Claude), and generates a **detailed CRO report** including:
- Executive summary  
- Issues & challenges  
- Quick wins  
- Detailed recommendations  
- Competitive comparison (if competitor URLs are provided)  
- HTML-formatted audit report (emailed automatically)  

## 🔧 Architecture
Refer to the included [Technical Architecture](./Technical-Architecture.md) file for details.  

Simplified flow:
Form Trigger → Split URLs → HTTP Request → Aggregate → Prepare Content → Claude Model → Format Report → Email Report

## ✨ Features
- **Multi-page comparison** (main vs competitors).  
- **AI-powered insights** (headlines, CTAs, trust signals, value props).  
- **Rich HTML report** automatically delivered via Gmail.  
- **Configurable** for different AI models, email recipients, or content sources.  

## 📦 Setup

### Requirements
- [n8n](https://n8n.io) v1.0+  
- Node.js runtime ES2020+  
- Accounts & credentials:
  - **Anthropic API key** (Claude models)  
  - **Gmail OAuth2** credentials (for sending email reports)

### Installation
1. Clone this repo:
   ```bash
   git clone https://github.com/yourusername/landing-page-cro-analyzer.git
   cd landing-page-cro-analyzer

2. Import the sanitized workflow JSON into n8n.
3. Create .env file from .env.example.
4. Configure credentials inside n8n for Gmail + Anthropic (use env variables).

**Environment Variables
**
See .env.example for the variables you need to configure.

**▶️ Usage
**
- Open the form trigger URL provided by n8n.

- Enter:

  - Landing Page URL
  - Competitor URLs (optional, comma-separated)

- Submit → Workflow runs → AI analysis → Email report delivered.

**📧 Output
**
- Email with:
  - Plain text summary
  - Full HTML CRO report (executive summary, issues, quick wins, recommendations, competitor comparison)

**🔒 Security
**
- All API keys and OAuth credentials are stored in n8n’s credential vault.
- Example .env file provided — never commit real keys to source control.

**🛠️ Development
**
- Modify the Prepare for Claude node to adjust how raw HTML/text is cleaned.
- Modify the Message a model node prompt for different output schemas.
- Modify the Format HTML Report node for styling or branding.
