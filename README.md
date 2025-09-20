# Firebase Studio

This is a NextJS starter in Firebase Studio.

## Project Overview and Evolution

This project, **SwasthyaGuide**, has evolved from a simple web-based chatbot into a more robust, multi-platform public health assistant. Here's a summary of its development journey and key features.

### Initial Foundation

The application started as a web-based chat interface with the following core components:

*   **Tech Stack**: Next.js, React, TypeScript, Tailwind CSS, and ShadCN UI for the frontend.
*   **AI Backend**: Google's Genkit and Gemini models power all conversational AI capabilities.
*   **Core Features**:
    *   **Multilingual Chat**: A fully functional chat interface supporting both English and Hindi.
    *   **AI-Powered Health Information**: The bot can answer general health questions, provide safe home remedies, and suggest simple, healthy recipes.
    *   **Symptom Checker**: A specialized mode to assess user-described symptoms and provide a basic risk evaluation.
    *   **Emergency Tools**: Features to find nearby hospitals using geolocation and view a list of public health updates.

### User Experience Enhancements

Based on feedback and to improve usability, several key features were added:

*   **Voice Interaction**: A microphone button was implemented for voice input, and text-to-speech was enabled for the bot's responses, making the conversation more natural and accessible.
*   **Automatic Scrolling**: The chat window was updated to automatically scroll to the latest message, creating a seamless user experience.

### WhatsApp Integration

To broaden the application's reach, SwasthyaGuide was integrated with WhatsApp using the Twilio API. This allows users to interact with the assistant directly from one of the world's most popular messaging apps.

*   A dedicated API endpoint (`/api/whatsapp`) was created to serve as a webhook for incoming messages from Twilio.
*   The same core Genkit `chat` flow is used to process messages and send replies back to the user on WhatsApp.

## WhatsApp Integration (via Twilio)

This application includes a feature to interact with the SwasthyaGuide assistant via WhatsApp using the Twilio API. To get this feature working, you need to configure your Twilio account and add the necessary credentials to the project.

### Configuration Steps

1.  **Create a Twilio Account**:
    *   Sign up for a free account at [twilio.com](https://www.twilio.com/).

2.  **Set Up the Twilio WhatsApp Sandbox**:
    *   From your Twilio Console, navigate to **Messaging > Try it out > Send a WhatsApp message**.
    *   Follow the on-screen instructions to connect your phone to the sandbox. You will need to send a specific code (e.g., `join-something-cool`) from your WhatsApp to the Twilio sandbox number.

3.  **Get Your Credentials**:
    *   On your Twilio Console dashboard, find your **Account SID** and **Auth Token**.
    *   The **Twilio Phone Number** is the sandbox number provided (e.g., `+14155238886`).

4.  **Set Environment Variables**:
    *   Create a new file named `.env.local` in the root of your project.
    *   Add the following lines to it, replacing the placeholder values with your actual Twilio credentials:
        ```env
        TWILIO_ACCOUNT_SID=ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
        TWILIO_AUTH_TOKEN=your_auth_token_from_twilio
        TWILIO_PHONE_NUMBER=whatsapp:+14155238886
        ```
    *   **Note**: The phone number must be prefixed with `whatsapp:`.

5.  **Configure the Webhook**:
    *   For Twilio to send incoming messages to your application, you must deploy your app to a public URL.
    *   In the Twilio WhatsApp Sandbox settings, find the section **"When a message comes in"**.
    *   Enter your application's public URL followed by `/api/whatsapp`. For example: `https://your-app-url.com/api/whatsapp`.
    *   Click **Save**.

After completing these steps, any message you send to the Twilio sandbox number from your connected phone will be processed by the application, and you will receive a response from the SwasthyaGuide assistant.
