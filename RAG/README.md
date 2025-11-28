# n8n RAG with Pinecone & Google Gemini

This project consists of two n8n workflows that implement a Retrieval-Augmented Generation (RAG) system using **Google Gemini** for embeddings and chat, **Pinecone** as the vector database, and **Google Drive** as the document source.

## Overview

The project is divided into two main workflows:

1.  **InsertKnowledgeBase.json**: This workflow ingests documents from a specified Google Drive folder. It downloads the files, splits the text into chunks, generates embeddings using Google Gemini, and upserts them into a Pinecone vector index.
2.  **RAG.json**: This is the AI Agent workflow. It receives a query (via webhook), retrieves relevant context from Pinecone using semantic search, and uses the Google Gemini Chat Model to answer the user's question based on the retrieved information.

## Features

*   **Automated Ingestion**: Fetches files directly from Google Drive.
*   **Semantic Search**: Uses Pinecone to store and retrieve relevant document chunks.
*   **AI-Powered Answers**: leverages Google Gemini to provide accurate answers based on your knowledge base.
*   **Memory**: Includes a simple memory buffer for the chat agent (in the RAG workflow) to handle follow-up questions.

## Prerequisites

Before you begin, ensure you have the following:

*   **n8n**: A running instance of n8n (Self-hosted or Cloud).
*   **Pinecone Account**: Sign up at [pinecone.io](https://www.pinecone.io/).
*   **Google Cloud Project**:
    *   **Gemini API (PaLM API)** enabled.
    *   **Google Drive API** enabled (for the ingestion workflow).
    *   **OAuth 2.0 Credentials** created for Google Drive access.

## Setup Guide

### 1. Pinecone Setup

1.  Log in to your Pinecone console.
2.  Create a new Index.
    *   **Name**: Choose a name (e.g., `knowledge-base`).
    *   **Dimensions**: `768` (This is the standard dimension for Google Gemini/PaLM embeddings).
    *   **Metric**: `Cosine` is usually recommended.

### 2. n8n Credentials Setup

You need to set up the following credentials in your n8n instance:

*   **Google Gemini(PaLM) Api**: API Key from Google AI Studio or Google Cloud.
*   **PineconeApi**: API Key from your Pinecone console.
*   **Google Drive OAuth2 API**: Client ID and Secret from Google Cloud Console (ensure the redirect URL matches your n8n instance).

### 3. Import Workflows

1.  Download the `InsertKnowledgeBase.json` and `RAG.json` files from this repository.
2.  In n8n, create a new workflow and select "Import from File" (or copy-paste the JSON content).
3.  Do this for both files.

### 4. Configuration

After importing, you will need to update the nodes with your specific details (placeholders have been added to the files):

**For `InsertKnowledgeBase`:**
*   **Pinecone Vector Store Node**:
    *   **Index Name**: Change `your-pinecone-index-name` to your actual Pinecone index name.
*   **Search files and folders (Google Drive) Node**:
    *   **Folder ID**: Change `YOUR_GOOGLE_DRIVE_FOLDER_ID` to the ID of the Google Drive folder you want to ingest.

**For `RAG`:**
*   **Pinecone Vector Store Node**:
    *   **Index Name**: Change `your-pinecone-index-name` to your actual Pinecone index name.
*   **Webhook Node**:
    *   The webhook path is set to `YOUR_WEBHOOK_PATH`. You can reset this to a default or custom unique path in the node settings.

### 5. Running the Project

1.  **Ingest Data**:
    *   Execute the `InsertKnowledgeBase` workflow manually (click "Execute Workflow").
    *   Verify in the Pinecone console that vectors have been added to your index.

2.  **Chat**:
    *   Activate the `RAG` workflow.
    *   Send a POST request to the Webhook URL with a body containing your query (e.g., `{"body": "What is the opening time of the clinic?"}`).
    *   Or, use the "Chat" interface if you are testing within n8n's Chat trigger (though this workflow uses a standard Webhook).

## Notes

*   **Credentials**: The JSON files in this repo have had their credential IDs sanitized (`YOUR_..._ID`). When you import them, n8n might ask you to select the correct credential from your own list.
*   **Models**: The workflows are configured for Google Gemini. If you wish to use OpenAI or others, you will need to replace the Chat Model and Embeddings nodes accordingly.
