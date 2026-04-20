📞 AI-Powered Hospital Appointment Booking System
(LLM-Driven Voice Call Booking Assistant)
📌 Overview

This system is an intelligent voice-based hospital appointment booking assistant powered by an LLM agent. The system handles the entire booking flow through a phone call, where the AI classifies user intent, validates inputs step-by-step, interacts with a database, and finalizes appointments automatically.

The system follows a controlled conversational state machine combined with LLM decision-making and backend tool calls.

🧠 Core Concept

Instead of a free-flow chatbot, the system uses a structured LLM pipeline:

LLM classifies every response (YES / NO / IRRELEVANT)
Conversation moves step-by-step
Backend APIs are triggered only when valid data is received
Call termination is enforced for repeated invalid inputs
🔄 Step-by-Step Workflow
📞 Step 1: Call Initiation

Patient calls the hospital system.

AI Voice Assistant says:

“Hello, I am the AI assistant for Dr. A. Would you like to book an appointment?”

🧠 Step 2: Intent Classification (LLM Layer)

Every user response is sent to LLM for classification:

YES → Proceed to next step
NO → Call is ended politely
IRRELEVANT → Retry counter increases
⚠️ Rule:
If IRRELEVANT response occurs multiple times consecutively → call is automatically terminated
📅 Step 3: Date Collection

If user says YES, system asks:

“Please provide your preferred date for the appointment.”

LLM processes response:

Converts natural language → structured date format (YYYY-MM-DD)
If invalid or irrelevant → retry classification
🏥 Step 4: Doctor Availability Check (Database Call)

Once valid date is received:

Backend performs:

Check if doctor is available on selected date
Query doctor schedule table
Validate working day
Output:
If doctor is NOT available → system informs user and ends flow or asks for another date
If available → proceed to slot fetching
⏰ Step 5: Slot Retrieval

System fetches available time slots:

Queries database for open slots
Removes already booked slots
Returns top 5 available slots

AI says:

“These are the available time slots: 10:00 AM, 11:30 AM, 2:00 PM, 4:00 PM, 6:00 PM. Please select one.”

🧾 Step 6: Slot Selection

User selects a slot via voice.

LLM:

Validates selection
Converts response into structured time format
Ensures it matches available slots

🔒 Step 7: Booking Confirmation (Database Transaction)

Once valid slot is selected:

System performs:

Atomic database transaction
Slot locking (prevents double booking)
Appointment record creation

💾 Step 8: Final Save

Database updates:

Appointment created
Doctor schedule updated
Slot marked as booked

📩 Step 9: Confirmation Response

AI responds:

“Your appointment with Dr. A has been successfully booked for [Date] at [Time].”

System also sends:

SMS confirmation
Email notification

📊 Step 10: Call Termination

Call ends after:

Successful booking OR
User rejection OR
Repeated invalid responses

⚙️ System Architecture
User Call
   ↓
Speech-to-Text Engine
   ↓
LLM Intent Classifier (YES / NO / IRRELEVANT)
   ↓
State Machine Controller
   ↓
Backend API (Doctor + Slot + Availability)
   ↓
Database (Appointments + Schedule)
   ↓
Confirmation Service (Voice + SMS + Email)

🧠 Key Intelligence Layers

🤖 LLM Responsibilities
Intent classification (YES / NO / IRRELEVANT)
Date normalization (natural language → structured date)
Slot validation
Conversation control

🧰 Backend Responsibilities
Doctor availability checking
Slot filtering
Appointment creation
Transaction-safe booking
Conflict prevention

🔒 Safety Rules
Multiple IRRELEVANT → call termination
NO response → immediate call end
Invalid slot → re-prompt user
Double booking prevention via locking

🚀 Why This System is Advanced
Real-world AI voice receptionist system
LLM used as decision classifier + controller
Hybrid architecture (LLM + rules + backend APIs)
Real-time scheduling with conflict handling
Production-level state management

💡 Real-World Use Cases
Hospitals
Clinics
Telemedicine systems
Automated receptionist replacement
24/7 appointment booking systems
📌 Summary

This project is a voice-driven AI appointment booking system that uses an LLM as a structured decision engine. It intelligently manages conversation flow, validates inputs, interacts with backend systems, and ensures safe, conflict-free appointment booking in real time.
