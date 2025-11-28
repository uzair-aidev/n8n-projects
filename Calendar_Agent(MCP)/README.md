# N8N Calendar Agent and MCP Server

This project contains two n8n workflows that work together to create a conversational AI agent for managing a Google Calendar.

## Introduction

The project consists of two main components:

1.  **Calendar Agent:** A chat-based interface that allows users to interact with the calendar agent. It uses a large language model (LLM) to understand user requests and execute actions.
2.  **Calendar MCP Server:** An n8n workflow that exposes a set of tools for creating, retrieving, updating, and deleting calendar events. The Calendar Agent communicates with this server to perform calendar operations.

## How it Works

The **Calendar Agent** workflow is triggered when a user sends a message. The message is processed by an agent that uses a large language model to understand the user's intent. The agent has access to the **Calendar MCP Server** tools, which it can use to perform actions on the user's behalf.

The **Calendar MCP Server** workflow is a separate n8n workflow that exposes a set of tools for interacting with a Google Calendar. These tools include:

*   `create_event`: Creates a new event in the calendar.
*   `get_events`: Retrieves a list of events from the calendar.
*   `UpdateEvent`: Updates an existing event in the calendar.
*   `DeleteEvent`: Deletes an event from the calendar.

When the Calendar Agent needs to perform a calendar operation, it makes a request to the Calendar MCP Server, which then executes the corresponding tool and returns the result to the agent.

## Setup Guide

To use these workflows, you will need to have an n8n instance set up. You will also need to have a Google Calendar that you want to manage.

1.  **Import the Workflows:**
    *   Import the `calendar_agent.json` and `calendar_mcp_server.json` files into your n8n instance.

2.  **Configure the Calendar MCP Server:**
    *   Open the `calendar_mcp_server` workflow.
    *   In the `UpdateEvent`, `DeleteEvent`, `get_events`, and `create_event` nodes, replace `REPLACE_WITH_YOUR_CALENDAR_ID` with the ID of your Google Calendar.
    *   You will also need to create credentials for the Google Calendar API and select them in each of the Google Calendar nodes.

3.  **Configure the Calendar Agent:**
    *   Open the `calendar_agent` workflow.
    *   In the `Calendar MCP Client` node, replace `REPLACE_WITH_YOUR_MCP_SERVER_SSE_ENDPOINT` with the SSE endpoint of your `calendar_mcp_server` workflow. You can get this from the `MCP Server Trigger` node in the `calendar_mcp_server` workflow.
    *   You will also need to create credentials for the Google Gemini API and select them in the `Google Gemini Chat Model` node.

4.  **Activate the Workflows:**
    *   Activate both the `calendar_agent` and `calendar_mcp_server` workflows.

Once you have completed these steps, you should be able to interact with your calendar by sending messages to the chat interface.
