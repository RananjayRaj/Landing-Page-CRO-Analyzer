# Technical Architecture: Landing Page CRO Analyzer

## Overview
This n8n workflow provides automated landing page Conversion Rate Optimization (CRO) analysis through intelligent content extraction, AI-powered competitive analysis, and automated HTML report delivery. The system transforms raw web page content into actionable CRO insights with professional email reporting.

## Architecture Components

### 1. Trigger & Orchestration Layer
- **Form Trigger Node**: Web-based form for URL submission with webhook endpoint
- **Workflow Orchestration**: Event-driven architecture supporting form submissions and API calls
- **Execution Context**: Maintains workflow state across processing stages

### 2. Data Acquisition Layer
- **Jina.ai Reader Integration**: Content extraction service for clean, readable page content
- **Multi-URL Processing**: Parallel processing of main landing page and competitor URLs
- **Connection Management**: HTTP request handling with custom headers for reliable scraping

### 3. Data Processing Engine
- **URL Splitting Node**: Separates main URL from competitor URLs with metadata tagging
  - Main page flagged with `is_main: true`
  - Competitor pages processed in parallel
- **Content Extraction**: Robust text extraction from various HTML structures
  - Handles nested objects and arrays
  - Extracts text from pageContent, body, data fields
  - Removes `[object Object]` artifacts
  - Truncates to 16,000 characters to manage token limits
- **Aggregation Node**: Combines all fetched pages into single payload for AI analysis

### 4. AI Analysis Engine
- **Primary AI Model**: Claude Sonnet for advanced CRO analysis
- **Analysis Framework**: Structured prompt engineering for consistent insights
  - Executive summary generation
  - Issues and challenges identification with impact assessment
  - Quick wins extraction (<30 minute implementations)
  - Detailed recommendations with priority levels (high/medium/low)
  - Competitive comparison analysis (when competitors provided)
- **Token Management**: Optimized 2000-token limit with structured JSON output formatting

### 5. Report Generation Engine
- **Dynamic HTML Email Composer**: JavaScript-based report generation
  - Responsive email template with embedded CSS styling
  - Color-coded priority badges (high=red, medium=yellow, low=blue)
  - Conditional sections (competitive comparison shown only if applicable)
  - Professional formatting with visual hierarchy
- **JSON Parsing with Fallbacks**: Multi-strategy parsing for AI responses
  - Direct JSON parsing
  - Markdown code fence extraction (```json ... ```)
  - Structured error handling with fallback templates

### 6. Output & Delivery Layer
- **Email Distribution**: Gmail integration with HTML formatting
  - Automated recipient management via environment variables
  - Rich HTML email with styling and formatting
  - Subject line: "Here's the full CRO Audit of your Landing Page 😊"
- **Attachment Support**: Complete HTML report in email body

## Data Flow Architecture

```
Form Trigger (URL Submission) →
Split URLs (Main + Competitors) →
HTTP Request (Jina.ai) [Parallel Processing] →
Aggregate (Combine All Pages) →
Prepare for Claude (Content Formatting) →
Message a Model (Claude Sonnet 4.5) →
Format HTML Report (Report Generation) →
Send Email Report (Gmail Delivery)
```

## Error Handling & Resilience

### Content Extraction Strategy
- **Multi-Field Fallback**: Tries multiple JSON fields for content extraction
- **Type Safety**: Handles strings, arrays, objects, and primitives
- **Depth Limiting**: Prevents infinite recursion with max depth of 3
- **Missing Data Handling**: Returns empty string rather than failing

### AI Response Parsing
- **Multi-Strategy Parsing**: Direct JSON, code fence extraction, fallback templates
- **Graceful Degradation**: Returns structured error messages when parsing fails
- **Debug Information**: Preserves raw AI response in `raw_model_text` field

## Performance Optimizations

### Memory Management
- **Content Truncation**: 16KB limit per page to prevent token overflow
- **Efficient Aggregation**: Minimal object creation during data combination
- **Streaming Processing**: Handles multiple URLs without memory bloat

### API Efficiency
- **Parallel URL Fetching**: Multiple pages fetched concurrently
- **Single AI Call**: All pages analyzed in one Claude request
- **Token Optimization**: Structured prompts for maximum output efficiency

## Integration Points

### External Services
- **AI Platform**: Anthropic Claude Sonnet 4.5 API
- **Content Extraction**: Jina.ai Reader (no API key required)
- **Email Service**: Gmail SMTP with OAuth2
- **Workflow Engine**: n8n automation platform

## Security Considerations

### Authentication Management
- **OAuth2 Implementation**: Secure Gmail integration
- **API Key Security**: Encrypted credential storage in n8n vault
- **No Stored Credentials**: Workflow JSON contains no secrets

### Data Protection
- **No Data Persistence**: Content processed in-memory only
- **Temporary Storage**: Page content exists only during workflow execution
- **Privacy Friendly**: No logging of analyzed URLs or content
