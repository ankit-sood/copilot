# Google Docs Assistant Setup Guide

This guide walks you through setting up the Google Developer Knowledge MCP server for use with GitHub Copilot in VS Code.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Step 1: Enable the Developer Knowledge API](#step-1-enable-the-developer-knowledge-api)
- [Step 2: Create and Configure an API Key](#step-2-create-and-configure-an-api-key)
- [Step 3: Enable MCP Server in Your Project](#step-3-enable-mcp-server-in-your-project)
- [Step 4: Configure GitHub Copilot](#step-4-configure-github-copilot)
- [Step 5: Set Up OAuth Client and Consent Screen](#step-5-set-up-oauth-client-and-consent-screen)
- [Testing Your Setup](#testing-your-setup)
- [References](#references)

## Prerequisites

Before you begin, ensure you have:
- A Google Cloud Platform project
- Access to Google Developer Knowledge MCP server
- VS Code with GitHub Copilot installed
- Appropriate permissions to enable APIs and create credentials in your GCP project

## Step 1: Enable the Developer Knowledge API

1. Open the [Developer Knowledge API page](https://console.cloud.google.com/apis/library) in the Google APIs library
2. Verify you have the correct project selected
3. Click **Enable**

> **Note:** No specific IAM roles are required to enable or use this API.

## Step 2: Create and Configure an API Key

### Create the API Key

1. Go to the [Google Cloud Console](https://console.cloud.google.com)
2. Select your project
3. Navigate to **APIs & Services** → **Credentials**
4. Click **Create credentials** → **API key**
5. Copy and save the generated API key

### Restrict the API Key

1. Click **Edit API key** (pencil icon) next to your newly created key
2. In the **Name** field, provide a descriptive name (e.g., "Developer Knowledge MCP Key")
3. Under **API restrictions**, select **Restrict key**
4. From the **Select APIs** dropdown, enable **Developer Knowledge API** and click **OK**
   
   > **Note:** If you just enabled the Developer Knowledge API, there may be a delay before it appears in the list.

5. Click **Save**

## Step 3: Enable MCP Server in Your Project

1. Open the Google Cloud Shell
2. Run the following command (replace `<projectId>` with your actual project ID):

   ```bash
   gcloud beta services mcp enable developerknowledge.googleapis.com --project=<projectId>
   ```

## Step 4: Configure GitHub Copilot

1. Open VS Code
2. Open GitHub Copilot Chat
3. Click the settings icon and select **MCP servers**
4. Add the following configuration:

   ```json
   {
     "mcp": {
       "servers": {
         "google-developer-knowledge": {
           "url": "https://developerknowledge.googleapis.com/mcp",
           "headers": {
             "X-Goog-Api-Key": "YOUR_API_KEY"
           }
         }
       }
     }
   }
   ```

5. Replace `YOUR_API_KEY` with the API key you created in Step 2

## Step 5: Set Up OAuth Client and Consent Screen

If this is your first time setting up OAuth, you'll need to configure the OAuth consent screen with callback URLs.

1. Go to [Google Auth Platform](https://console.cloud.google.com/apis/credentials)
2. Select **Clients** from the left navigation pane
3. Click **Create Client**
4. Configure the client:
   - **Application type:** Web Application
   - **Name:** MCPClientVsCode (or any descriptive name)
   - **Authorized redirect URIs:** Add both:
     - `https://vscode.dev/redirect`
     - `http://127.0.0.1:33418`
5. Click **Save**
6. Copy the Client ID for future reference

## Testing Your Setup
You can verify your setup by testing the MCP endpoint:

```bash
curl --location 'https://developerknowledge.googleapis.com/mcp' \
  --header 'content-type: application/json' \
  --header 'accept: application/json, text/event-stream' \
  --header 'X-Goog-Api-Key: YOUR_API_KEY' \
  --data '{
    "method": "tools/list",
    "jsonrpc": "2.0",
    "id": 1
  }'
```

This command should return a list of available tools if everything is configured correctly.

## References

- [Official Documentation](https://developers.google.com/knowledge/mcp#github-copilot-in-vs-code)
- [MCP Reference](https://developers.google.com/knowledge/reference/mcp)
- [Developer Knowledge API](https://developers.google.com/knowledge)