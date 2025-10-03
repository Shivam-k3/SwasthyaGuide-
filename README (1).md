# Firebase Studio

This is a NextJS starter in Firebase Studio.

## Project Overview and Evolution

This project, **SwasthyaGuide**, has evolved from a simple web-based chatbot into a more robust, multi-platform public health assistant. Here's a summary of its development journey and key features.

### Initial Foundation & Core Features

The application started as a web-based chat interface with the following core components:

*   **Tech Stack**: Next.js, React, TypeScript, Tailwind CSS, and ShadCN UI for the frontend.
*   **AI Backend**: Google's Genkit and Gemini models power all conversational AI capabilities.
*   **Core Features**:
    *   **Multilingual Chat**: A fully functional chat interface supporting both English and Hindi. The AI can answer general health questions, provide safe home remedies, and suggest simple, healthy recipes.
    *   **Mental Health Crisis Detection**: The AI is trained to recognize signs of a mental health crisis. If detected, it immediately provides contact information for emergency helplines.
    *   **Symptom Checker**: A specialized mode to assess user-described symptoms, provide a basic risk evaluation, and identify potential signs of an allergic reaction.
    *   **Emergency SOS Button**: A prominent SOS button gives users immediate access to emergency helpline numbers and a feature to find nearby hospitals using their device's geolocation.

### Scalable & Modular Design

The application is built with a scalable and modular architecture in mind.

*   **Extensible Chatbot**: The AI is designed to be easily extensible. Its knowledge base already includes key public health topics such as **mental health**, **maternal and child health (MCH)**, **sexual health**, and common illnesses like **fever, dengue, and TB**. New modules and health topics can be added without altering the core architecture.
*   **Distinct Modules**: Features like the **Diet Advisor**, **Report Analyzer**, and **MDR Risk Assessment** function as independent modules within the "Health Feed," demonstrating the ease with which new capabilities can be integrated.
*   **Hospital Module Concept**: The "MDR Pathogen Screening" feature is a conceptual module intended for a separate, enterprise-grade hospital application. It would require its own backend and secure integration with hospital IT systems, making it distinct from the public-facing SwasthyaGuide assistant.

### User Experience Enhancements & The Health Feed

To improve usability and expand functionality, several key features were added, many of which are housed in the "Health Feed" slide-out panel:

*   **Voice Interaction**: A microphone button was implemented for voice input, and an empathetic text-to-speech voice was enabled for the bot's responses, making the conversation more natural and accessible.
*   **Report Analyzer**: Users can upload an image of a medical report, and the AI provides a simplified, easy-to-understand summary.
*   **Diet Advisor**: A dedicated tool that suggests a single, healthy meal with a recipe based on the user's dietary preference (e.g., vegetarian).
*   **Myth Buster**: A fact-checking tool where users can enter a health claim to see if it's a myth or a fact.
*   **Offline-Accessible Information**:
    *   **Health Schemes**: Provides detailed information on major public health schemes in India.
    *   **Medical Rights**: Informs users about their rights as patients.
*   **Public Health Updates & Alerts**: A feed that displays the latest public health advisories and news, with critical alerts highlighted for visibility.

### Multi-Platform Integration

SwasthyaGuide is accessible across multiple platforms to ensure wide reach.

*   **React Web App**: The primary interface is a responsive web application built with Next.js and React.
*   **WhatsApp & SMS Integration**: The application is integrated with the Twilio API to support both WhatsApp and standard SMS. This allows users to interact with the assistant directly from one of the world's most popular messaging apps or via a simple text message, ensuring functionality even in low-bandwidth areas.
*   **Future Mobile App**: The web app is built to be mobile-first and can be packaged into a native mobile app for the Google Play Store and Apple App Store using a tool like Capacitor.

## Twilio Integration (WhatsApp & SMS)

This application includes a feature to interact with the SwasthyaGuide assistant via WhatsApp or SMS using the Twilio API. To get this feature working, you need to configure your Twilio account and add the necessary credentials to the project.

### Configuration Steps

1.  **Create a Twilio Account**:
    *   Sign up for a free account at [twilio.com](https://www.twilio.com/).

2.  **Get a Twilio Phone Number**:
    *   From your Twilio Console, navigate to the **Phone Numbers** section and get a new number. This number can be used for both SMS and can be linked to the WhatsApp sandbox.

3.  **Set Up the Twilio WhatsApp Sandbox**:
    *   Navigate to **Messaging > Try it out > Send a WhatsApp message**.
    *   Follow the on-screen instructions to connect your phone to the sandbox. You will need to send a specific code (e.g., `join-something-cool`) from your WhatsApp to the Twilio sandbox number.

4.  **Get Your Credentials**:
    *   On your Twilio Console dashboard, find your **Account SID** and **Auth Token**.
    *   For the **`TWILIO_PHONE_NUMBER`** environment variable, you will use the number you acquired in Step 2.
        *   For **WhatsApp**, the value should be `whatsapp:+14155238886` (using the official Twilio Sandbox number).
        *   For **SMS**, the value should be the phone number you acquired, e.g., `+1YourTwilioNumber`. You can use the same variable, but you'll need to decide which channel is your primary one for sending messages *from* the app if ever needed, though this webhook handles replies automatically.

5.  **Set Environment Variables**:
    *   Create a new file named `.env.local` in the root of your project.
    *   Add the following lines, replacing the placeholder values:
        \'\'\'env
        TWILIO_ACCOUNT_SID=ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
        TWILIO_AUTH_TOKEN=your_auth_token_from_twilio
        # For WhatsApp, use the sandbox number. For SMS, use your Twilio number.
        TWILIO_PHONE_NUMBER=whatsapp:+14155238886 
        \'\'\'

6.  **Configure the Webhook**:
    *   For Twilio to send incoming messages to your application, you must deploy your app to a public URL.
    *   Go to your Twilio phone number's configuration page. Under the **"Messaging"** section, find the setting for **"A MESSAGE COMES IN"**.
    *   Set the webhook URL to your application's public URL followed by `/api/whatsapp`. For example: `https://your-app-url.com/api/whatsapp`.
    *   This same webhook will now process both incoming WhatsApp messages and SMS messages sent to this number.

After completing these steps, any message you send to your Twilio number (via SMS) or the Twilio sandbox number (via WhatsApp) will be processed by the application, and you will receive a response from the SwasthyaGuide assistant.

## Conceptual Solution: Hospital Infection Control

This project includes a conceptual prototype for a hospital infection control system, designed to address the challenge of tracking and preventing Multi-Drug Resistant (MDR) pathogen outbreaks.

### The Problem

MDR pathogens pose a significant threat in healthcare settings. Manual tracking of patient contacts and risk factors is often inefficient and too slow to prevent outbreaks. A digital solution is needed to automate this process, enabling real-time risk assessment and early intervention.

### Our Conceptual Solution

SwasthyaGuide includes two key modules that serve as a proof-of-concept for a larger, integrated hospital IT system. These tools simulate the core logic of an infection control system in a safe, standalone environment.

1.  **MDR Risk Assessment Module**:
    *   **Function**: Allows a user (e.g., a healthcare professional) to input a patient's symptoms and select from a list of known risk factors (like recent ICU stays or antibiotic use).
    *   **Output**: An AI model assesses this information and provides a preliminary risk level (Low, Medium, or High), an explanation for the assessment, and a list of recommended infection control precautions (e.g., "Contact Precautions," "Standard Precautions").
    *   **Purpose**: Demonstrates how AI can be used to standardize and automate preliminary risk screening based on patient data.

2.  **MDR Pathogen Screening Module**:
    *   **Function**: Simulates the tracking of a patient's movement within a hospital. A user can enter a patient ID and select the wards they have recently visited (e.g., ICU, Surgical Ward).
    *   **Output**: The AI simulates a real-time alert, flagging a potential exposure chain based on high-risk locations. For example, it might generate an alert like: "High-risk alert: Potential exposure to Carbapenem-resistant pathogen in ICU. Recommend patient isolation and follow-up with infection control team."
    *   **Purpose**: This demonstrates the core logic of a real-time alerting system that could be triggered by data from a hospital's EHR, lab, or IT systems.

These modules are intentionally designed to be **conceptual and not connected to live patient data**. They prove the viability of using an AI-driven, modular approach to tackle the complex challenge of hospital infection control. They are located in the "Hospital Tools" section of the Health Feed to distinguish them from the public-facing features.
