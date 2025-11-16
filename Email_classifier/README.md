# Email Classifier n8n Workflow

This workflow automates the classification and labeling of incoming emails in your Gmail account. It uses AI to categorize emails and applies corresponding labels, helping you prioritize and manage your inbox more efficiently.

## Workflow Function

The workflow performs the following actions:

1.  **Triggers on Email Reception:** The workflow starts automatically when a new email is received in your specified Gmail account.
2.  **Classifies Email Content:** It then uses a Large Language Model (LLM) to classify the email content into one of three categories: "High," "Medium," or "Low" priority.
3.  **Applies Gmail Labels:** Based on the classification, the workflow applies the corresponding label ("High Priority," "Medium Priority," or "Low Priority") to the email in your Gmail account.
4.  **Sends WhatsApp Notification (for High Priority):** If an email is classified as "High Priority," the workflow sends a notification to your WhatsApp number.

## Nodes Used

This workflow uses the following n8n nodes:

*   **Gmail Trigger:** To start the workflow when a new email is received.
*   **Google Gemini Chat Model:** To power the AI-based email classification.
*   **Email Classifier:** A custom node to classify the email content.
*   **Gmail:** To apply labels to the emails.
*   **WhatsApp:** To send notifications for high-priority emails.

## Setup Guide

To use this workflow, you need to have an n8n instance set up and have the necessary credentials for the following services:

*   Gmail
*   Google Gemini (or another LLM provider)
*   WhatsApp

Here's how to set up the workflow:

1.  **Import the Workflow:** Download the `Email_classifier.json` file and import it into your n8n instance.
2.  **Configure the Gmail Trigger:**
    *   Open the "Email Received" node.
    *   Select your Gmail account from the credentials dropdown.
    *   Configure the trigger settings as needed (e.g., specify a folder to watch).
3.  **Configure the Google Gemini Chat Model:**
    *   Open the "Google Gemini Chat Model" node.
    *   Select your Google Gemini API credentials from the dropdown.
4.  **Configure the Gmail Nodes:**
    *   Open the "High Priority," "Medium Priority," and "Low Priority" nodes.
    *   Select your Gmail account from the credentials dropdown.
    *   Make sure the label IDs in the "Label Ids" field correspond to the labels you want to use in your Gmail account. You can find the label IDs in your Gmail settings.
5.  **Configure the WhatsApp Node:**
    *   Open the "Whatsapp Message" node.
    *   Configure the node to send a message to your desired phone number.
6.  **Activate the Workflow:** Once you have configured all the nodes, activate the workflow.

Now, the workflow will automatically classify and label your incoming emails.
