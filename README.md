# PiggyBack

**A robotic desk companion that helps users curb impulse purchases.**

PiggyBack gives online spending a physical presence. By combining a Chrome extension, an AI-powered backend, and an expressive robotic companion, PiggyBack encourages users to pause and reconsider purchases before checking out.

Built for MakeCU 2026, Columbia University's hardware hackathon.

**Demo:**
https://youtu.be/cQtnAv6WNG0

## The Problem

Online shopping makes spending feel invisible and frictionless. Targeted advertisements, promotional offers, and one-click checkout make impulse purchases easy.

Traditional budgeting tools track spending after the fact. PiggyBack takes a different approach: it intervenes at the moment of purchase.

## The Solution

PiggyBack is a robotic desk companion that acts as an accountability partner during online shopping.

### How It Works

1. **Detect:** A Chrome extension monitors shopping behavior, including ad referrals, sponsored listings, sales, and cart activity.
2. **Intercept:** When a user attempts to check out, the extension pauses the purchase.
3. **Question:** PiggyBack initiates an AI-powered conversation, asking users to explain their purchase.
4. **React:** The robot responds through facial expressions, head movements, and spoken dialogue.
5. **Decide:** Based on the conversation and budget rules, PiggyBack approves the purchase, introduces a cooling-off period, or escalates the decision.
6. **Reflect:** A dashboard tracks spending, savings goals, and previous purchase decisions.

## Key Features

- **Checkout Intervention:** Pauses checkout to encourage users to reconsider purchases.
- **Shopping Behavior Detection:** Identifies ad referrals, sponsored products, upselling, cart activity, and promotional offers.
- **AI-Powered Conversations:** Uses Gemini to generate contextual questions and purchase recommendations.
- **Expressive Robot:** ESP32-controlled OLED eyes and servos communicate PiggyBack's reactions.
- **Voice Interaction:** Supports spoken responses through speech recognition and text-to-speech.
- **Eye-Contact Detection:** Uses computer vision to track the user's face and eye contact.
- **Budget Dashboard:** Tracks monthly spending, savings goals, purchase history, and items users are reconsidering.

## Architecture

\`\`\`text
Chrome Extension
       |
       | WebSocket / HTTP
       v
FastAPI Backend (brain.py)
       |
       +---- Gemini AI
       +---- Shopping Analysis (sales.py)
       +---- Budget & History (store.py)
       +---- Computer Vision (vision.py)
       +---- Dashboard (dashboard.html)
       |
       | USB Serial
       v
ESP32 Robot
       |
       +---- OLED Eyes
       +---- Neck Servos
\`\`\`

## Tech Stack

| Component | Technologies |
|---|---|
| Browser Extension | JavaScript, Chrome Manifest V3 |
| Backend | Python, FastAPI, WebSockets |
| AI | Gemini |
| Speech | faster-whisper, Text-to-Speech |
| Computer Vision | MediaPipe, OpenCV |
| Hardware | ESP32, Arduino, OLED Displays, Servos |
| Browser Automation | Playwright |
| Dashboard | HTML, CSS, JavaScript |

## Project Structure

- `extension/` – Chrome extension and shopping behavior detection.
- `brain.py` – Backend conversation logic and hardware communication.
- `sales.py` – Sale and cart analysis.
- `store.py` – Budget, savings goals, and purchase history.
- `vision.py` – Face tracking and eye-contact detection.
- `dashboard.html` – Spending and savings dashboard.
- `firmware/` – ESP32 firmware controlling the robot.
- `bot/` – Optional Playwright shopping browser monitor.
- `store/` – Demo shopping storefront.

## Getting Started

### Requirements

- Python 3.12
- Google Chrome
- Gemini API credentials
- ESP32 hardware (optional for software-only testing)
- Webcam and microphone for voice and vision features

### 1. Clone the Repository

\`\`\`bash
git clone https://github.com/alishachang2/piggyback.git
cd piggyback
\`\`\`

### 2. Set Up the Environment

\`\`\`bash
python3.12 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
\`\`\`

### 3. Configure API Credentials

Create a `.env` file in the repository root.

\`\`\`env
GEMINI_API_KEY=your_api_key
GEMINI_API_KEY_WEB=your_web_api_key
\`\`\`

Never commit API keys.

For testing without an API key, use mock mode.

### 4. Start the Backend

\`\`\`bash
uvicorn brain:app --port 8000
\`\`\`

Visit:
- Dashboard: http://localhost:8000/
- Demo Store: http://localhost:8000/store/

### 5. Install the Chrome Extension

1. Navigate to `chrome://extensions`.
2. Enable Developer Mode.
3. Select Load Unpacked.
4. Select the `extension/` directory.
5. Visit the demo store.

See `extension/README.md` for additional instructions.

## Limitations

PiggyBack is a hackathon prototype. Shopping-page detection and checkout interception may vary across retailers. The optional Playwright monitor currently supports retailer-specific cart extraction for Amazon, Target, and Walmart. The local dashboard is not authenticated and should not be exposed publicly without additional security measures.

The project does not connect to bank accounts or execute purchases.

## Product Vision

PiggyBack explores how physical interaction and conversational AI can encourage more intentional digital behaviors.

By transforming an invisible online transaction into an interactive experience, PiggyBack aims to make users more conscious of their spending decisions.
