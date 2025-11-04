# 💈 Barber Shop Assistant (AI Agent + Cal.com + Twilio WhatsApp)

This project is an intelligent **AI-powered Barber Shop Assistant** that can handle:
- 💬 WhatsApp chat booking via **Twilio**
- 📅 Real-time appointment creation using **Cal.com API**
- 🧠 Contextual conversations and service selection
- 💻 Optional console-based interaction mode for local testing

---

## 🚀 Features

✅ List available barbers and their services  
✅ Interactive WhatsApp booking flow  
✅ Date/time parsing and formatting (ISO8601 with UTC `Z` suffix)  
✅ Create Cal.com bookings programmatically  
✅ Flask server integration for WhatsApp webhooks  
✅ Local console mode for testing without Twilio  

---

## ⚙️ Folder Structure

📦 Barber-Customer-Service-Ver2
├── main.py # Entry point (Flask + Console)
├── tools.py # Cal.com API + Helper functions
├── agent.py # Chat logic handler
├── requirements.txt # Dependencies
├── README.md # Project documentation
└── ...

yaml
Copy code

---

## 🧩 Setup Instructions

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/kaustav812004/Barber-Customer-Service-Ver2.git
cd Barber-Customer-Service-Ver2
2️⃣ Create a Virtual Environment
bash
Copy code
python -m venv venv
venv\Scripts\activate      # On Windows
# or
source venv/bin/activate   # On macOS/Linux
3️⃣ Install Dependencies
bash
Copy code
pip install -r requirements.txt
4️⃣ Environment Variables (optional for local)
Create a .env file in your root directory with the following:

ini
Copy code
CALCOM_API_KEY=your_calcom_api_key_here
TWILIO_ACCOUNT_SID=your_twilio_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
💻 Running Locally (Console Mode)
To run in console mode (no Twilio, direct terminal chat):

bash
Copy code
python main.py
You’ll see:

diff
Copy code
=== Barber Shop Assistant ===
Please enter your name:
Then you can pick options like:

markdown
Copy code
1. Pricing Inquiry
2. Book Appointment
3. Complaint
4. General Chat
5. Exit
💬 WhatsApp Integration (Twilio + ngrok)
Step 1: Start Flask Server
bash
Copy code
python main.py whatsapp
This runs the Flask webhook on port 5000 by default.

Step 2: Start ngrok Tunnel
Go to your ngrok installation directory and run:

bash
Copy code
ngrok http 5000
You’ll get a forwarding URL like:

nginx
Copy code
Forwarding https://a1b2c3d4.ngrok.io -> http://localhost:5000
Step 3: Configure Twilio WhatsApp Sandbox
Go to your Twilio Console → Messaging → WhatsApp Sandbox.

Set the Webhook URL to:

bash
Copy code
https://a1b2c3d4.ngrok.io/whatsapp
Save the configuration.

Send “book” to your Twilio WhatsApp number to start the interaction!

🧠 WhatsApp Conversation Flow
User → Bot Interaction Example:

vbnet
Copy code
User: book
Bot: Great! Let's book your appointment.
Available barbers:
- Rahul
- Amit
- Sneha
Please reply with the barber name.

User: Rahul
Bot: Rahul offers: Haircut, Beard Trim
Please reply with the service you want.

User: Haircut
Bot: Please provide appointment datetime in format YYYY-MM-DD HH:MM (e.g. 2025-11-04 16:30)

User: 2025-11-04 16:30
Bot: Appointment confirmed!
Barber: Rahul
Service: Haircut
Time: 2025-11-04T16:30:00Z
🧾 Function Reference
format_datetime(user_input)
Converts user’s date/time input (YYYY-MM-DD HH:MM) → ISO8601 UTC (e.g. 2025-11-04T16:30:00Z)

tools.list_barbers()
Returns all available barbers and services.

tools.create_booking()
Creates a Cal.com booking via API using:

python
Copy code
tools.create_booking(event_type_id, start, timezone, name, email, barber, service)
🧱 Tech Stack
Python 3.10+

Flask – Server backend

Twilio – WhatsApp API integration

Cal.com API – Appointment scheduling

ngrok – Local tunneling for webhook

Datetime & pytz – Timezone management

🧑‍💻 Developer Notes
To extend this project:

Modify tools.py for additional API endpoints.

Edit agent.py for richer conversational responses.

Update main.py to support new service categories or extra steps in the booking flow.

📜 License
This project is released under the MIT License.
