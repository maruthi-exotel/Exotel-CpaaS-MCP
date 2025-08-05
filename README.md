# Exotel MCP Server

A Model Context Protocol (MCP) server that provides seamless integration between Claude AI and Exotel's communication APIs for SMS and voice calling services.

## Features

- 📱 **SMS Services**: Send single, bulk, and dynamic SMS messages with DLT compliance
- ☎️ **Voice Calling**: Initiate voice calls, connect numbers, and integrate with call flows
- 📊 **Status Tracking**: Real-time delivery status and callback management
- 🔐 **Secure Authentication**: Token-based authentication system
- 🤖 **Claude AI Integration**: Direct integration with Claude through MCP protocol

## Table of Contents

- [Prerequisites](#prerequisites)
- [Configuration](#configuration)
- [Usage](#usage)
- [API Services](#api-services)
- [Authentication](#authentication)
- [Support](#support)

## Prerequisites

Before using the Exotel MCP Server, ensure you have:

- **Claude Desktop App**: Latest version installed
- **Node.js and npm**: Required for MCP remote connection
- **Exotel Account**: Active account with API credentials
- **MCP Remote Package**: Install if not already available

### Installing MCP Remote

If you don't have `mcp-remote` installed, run:

```bash
npm install -g mcp-remote
```

Verify installation:
```bash
npx mcp-remote --version
```

## Configuration

### Claude Desktop Configuration

To integrate Exotel MCP Server with Claude, add the following configuration to your Claude desktop settings:

**Location**: Claude Desktop → Settings → Developer → Edit Config

```json
{
  "mcpServers": {
    "exotel": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "http://ec2-13-127-242-200.ap-south-1.compute.amazonaws.com:8080/mcp",
        "--allow-http",
        "--header",
        "Authorization:${AUTH_HEADER}"
      ],
      "env": {
        "AUTH_HEADER": "{'token':'YOUR_EXOTEL_TOKEN','from_number':'YOUR_FROM_NUMBER','dlt_temp':'YOUR_DLT_TEMPLATE','dlt_entity':'YOUR_DLT_ENTITY','caller_id':'YOUR_CALLER_ID','api_domain':'https://api.exotel.com','account_sid':'YOUR_ACCOUNT_SID','exotel_portal_url':'http://my.exotel.com'}"
      }
    }
  }
}
```

### Required Credentials

Replace the placeholder values with your actual Exotel credentials:

#### **YOUR_EXOTEL_TOKEN**: Base64 Encoded API Credentials

This token is created by encoding your Exotel API Key and Secret in Base64 format.

**Step 1: Get your API credentials from Exotel Dashboard**
1. Log into your [Exotel Dashboard](https://my.exotel.com/)
2. Navigate to **Settings** → **API Settings**
3. Copy your **API Key** and **API Secret**

**Step 2: Create the Base64 token**

Format: `api_key:api_secret` (colon-separated)

**Example**: If your API Key is `abc123` and API Secret is `xyz789`, combine them as: `abc123:xyz789`

**Step 3: Encode to Base64**

You can use any of these methods:

**Online Tool:**
- Visit [base64encode.org](https://www.base64encode.org/)
- Enter your `api_key:api_secret` string
- Copy the encoded result

**Command Line (Mac/Linux):**
```bash
echo -n "your_api_key:your_api_secret" | base64
```

**Command Line (Windows):**
```powershell
[Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes("your_api_key:your_api_secret"))
```

#### **Other Required Values:**

- **YOUR_FROM_NUMBER**: Your registered Exotel phone number (from Dashboard → Numbers)
- **YOUR_DLT_TEMPLATE**: DLT template ID for SMS compliance (from Dashboard → DLT)
- **YOUR_DLT_ENTITY**: DLT entity ID for SMS compliance (from Dashboard → DLT)
- **YOUR_CALLER_ID**: Your registered caller ID (from Dashboard → Numbers)
- **YOUR_ACCOUNT_SID**: Your Exotel account SID (from Dashboard → API Settings)

## Usage

Once configured, you can use Claude to interact with Exotel services using natural language commands. Simply describe what you want to do, and Claude will handle the API calls through the MCP server.

**Example Commands:**
- "Send an SMS to +919999999999 saying 'Hello from Claude!'"
- "Call +919999999999"
- "Check the delivery status of my last SMS"
- "Connect +919999999999 with +919888888888"

## API Services

### SMS Services

#### Send Individual SMS
Send a single SMS message to a specific phone number with DLT compliance.

**Example**: 
```
Send an SMS to +919999999999 with message "Hello from Claude!" using DLT template 1107160086208866373 and entity 1101428740000012125
```

#### Send Bulk SMS (Same Message)
Send the same message to multiple recipients at once.

**Example**: 
```
Send "Welcome to our service!" to these numbers: +919999999999, +919888888888, +919777777777
```

#### Send Dynamic Bulk SMS
Send personalized messages to multiple recipients with different content for each.

**Example**: 
```
Send personalized messages: "Hello John" to +919999999999 and "Hello Jane" to +919888888888
```

### Voice Services

#### Make Voice Call
Initiate a voice call to any phone number using your registered Exotel number.

**Example**: 
```
Call +919999999999 from my registered number
```

#### Connect Two Numbers
Bridge two phone numbers in a single call, connecting them together.

**Example**: 
```
Connect +919999999999 with +919888888888 in a conference call
```

#### Call Flow Integration
Connect a phone number to a predefined Exotel call flow or IVR system.

**Example**: 
```
Connect +919999999999 to call flow app_id 12345
```

### Status & Tracking Services

#### Check SMS Delivery Status
Get real-time delivery status and details for sent SMS messages.

**Example**: 
```
Check the delivery status of SMS sent to +919999999999
```

#### Check Voice Call Status
Retrieve call details, duration, and status for voice calls.

**Example**: 
```
Get call details for calls made to +919999999999
```

#### Get Call History
Retrieve bulk call details and history for analysis.

**Example**: 
```
Get all call details made from +919999999999
```

#### Number Information
Get metadata and information about phone numbers.

**Example**: 
```
Get information about phone number +919999999999
```

## Authentication

The Exotel MCP Server uses secure token-based authentication. All your Exotel credentials are configured in the Claude desktop configuration and are used to authenticate with Exotel's APIs.

### Security Features

- **Secure Token Handling**: Your Exotel API tokens are securely processed
- **User Isolation**: Each user's data is kept separate and secure
- **DLT Compliance**: Built-in support for DLT (Distributed Ledger Technology) requirements for SMS in India

### Getting Your Exotel Credentials

1. **Log into your [Exotel Dashboard](https://my.exotel.com/)**
2. **Navigate to Settings → API Settings** to get your API Key, API Secret, and Account SID
3. **Go to Numbers section** to note your registered phone numbers and caller IDs
4. **Visit DLT section** to get your DLT Template and Entity IDs (required for SMS compliance in India)
5. **Create your Base64 token** using the API Key and Secret as detailed in the [Configuration](#configuration) section

All these credentials should be properly formatted and added to your Claude configuration as shown above.

## Support

### Getting Help

- **Configuration Issues**: Double-check your Exotel credentials and Claude configuration
- **API Usage**: Refer to the [API Services](#api-services) section for usage examples
- **Exotel Account**: Contact Exotel support for account-related issues
- **DLT Compliance**: Ensure your DLT templates and entity IDs are properly registered

### Common Issues

#### "Connection Failed" Error
- Verify your `mcp-remote` installation: `npx mcp-remote --version`
- Check your internet connection
- Ensure Claude Desktop is updated to the latest version

#### "Authentication Failed" Error
- Verify your Exotel API token is correctly Base64 encoded from `api_key:api_secret` format
- Double-check your API Key and API Secret from Exotel Dashboard → Settings → API Settings
- Ensure the colon (`:`) separator is included between API Key and Secret before encoding
- Check that your account SID matches your Exotel account
- Ensure your phone numbers are properly registered with Exotel

#### SMS Not Delivered
- Verify DLT template and entity IDs are correct
- Check that your message content matches the registered DLT template
- Ensure the recipient number is valid and reachable

### Resources

- **Exotel Documentation**: [https://developer.exotel.com/](https://developer.exotel.com/)
- **DLT Information**: [https://www.trai.gov.in/](https://www.trai.gov.in/)
- **Claude Desktop**: [https://claude.ai/](https://claude.ai/)

---

🚀 **Ready to get started?** Configure your credentials and start sending SMS and making calls through Claude AI!
