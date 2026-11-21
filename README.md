# 🎟️ EventSphere — Online Event Booking Platform

EventSphere is a web-based event discovery and booking platform that helps users explore events, reserve tickets, and access digital tickets in one place. It provides separate Customer and Organizer dashboards, UPI QR-based payment instructions, organizer-reviewed payment references, and QR-code ticket generation.

### Screenshot

<img width="1900" height="907" alt="Screenshot 2026-11-21 164206" src="https://github.com/user-attachments/assets/e26576d9-a8b0-4845-a2d0-2c61db0ccc5d" />

## ✨ Features

### 👤 Customer Dashboard
- 📝 Register and log in to a customer account.
- 🔍 Browse and search available events.
- 📅 View event details and ticket availability.
- 🎫 Reserve event tickets.
- 📱 Generate a UPI QR code with the booking amount and a limited payment window.
- 💳 Submit a UPI transaction reference (UTR) for organizer review.
- 📋 View booking history and booking status.
- 🎟️ Download digital tickets containing verification QR codes.

### 🏢 Organizer Dashboard
- 🔐 Register and log in to an organizer account.
- ➕ Create and publish events.
- 🛠️ Manage event information and ticket availability.
- 💰 Provide UPI ID for receiving event payments.
- 📊 View customer bookings and payment requests.
- 🔎 Review submitted UPI transaction references (UTR).
- ✅ Approve or ❌ reject payment requests.
- 👥 Manage event bookings and attendees.

## 🛠️ Technology Stack

| Part | Technology |
|---|---|
| 💻 Frontend | React, Vite, JavaScript, CSS |
| ⚙️ Backend | Python, Flask |
| 🗄️ Database | SQLite by default; configurable through `DATABASE_URL` |
| 🔐 Authentication | JWT (JSON Web Tokens) |
| 📱 QR Codes | Python `qrcode` package |
| 🔗 API Communication | REST API |

## 📂 Project Structure

```text
EventSphere/
├── client/                 # React + Vite frontend
│   ├── src/
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── styles.css
│   ├── .env.example
│   ├── package.json
│   └── vite.config.js
│
├── server/                 # Flask backend and API
│   ├── app.py
│   ├── requirements.txt
│   └── .env.example
│
├── instance/               # Local SQLite database files, if created here
└── README.md
```

## 📋 Requirements

Install the following before running the project:

- 🐍 Python 3.10 or later
- 🟢 Node.js and npm
- 💻 Visual Studio Code (recommended)

## 🚀 Run the Project in VS Code

### 1️⃣ Open VS Code

1. Open VS Code.
2. Click **File → Open Folder**.
3. Select your `EventSphere` project folder (the folder containing `client` and `server`).
4. Open **Terminal → New Terminal**.

### 2️⃣ Start Backend

Open the first VS Code terminal and move into the backend folder:

```powershell
cd server
```

Activate the virtual environment. If it does not exist, create it first using `python -m venv venv` from the project root or `py -m venv venv`:

```powershell
.\venv\Scripts\Activate.ps1
```

If your virtual environment is in the main project folder instead of `server`, use:

```powershell
..\venv\Scripts\Activate.ps1
```

Install backend dependencies (first time only):

```powershell
pip install -r requirements.txt
```

If you have not created your environment file yet, copy the example file from the `server` folder:

```powershell
Copy-Item .env.example .env
```

Start the backend:

```powershell
python app.py
```

🌐 **Backend URL:** http://127.0.0.1:5000

### 3️⃣ Start Frontend

Keep the backend terminal running. Open a second terminal using the **+** icon in the VS Code Terminal panel.

Move into the frontend folder:

```powershell
cd client
```

Install frontend dependencies (first time only):

```powershell
npm install
```

If you have not created your frontend environment file yet, copy the example file:

```powershell
Copy-Item .env.example .env
```

Start the frontend development server:

```powershell
npm run dev
```

🌐 **Frontend URL:** http://localhost:5173

Open the frontend URL in your browser. Both backend and frontend terminals must remain running while you use the application.

### 4️⃣ Final Workflow

| Task | Command |
|---|---|
| ⚙️ Start backend | `python app.py` (from `server`) |
| 💻 Start frontend | `npm run dev` (from `client`) |
| 🛑 Stop either server | `Ctrl + C` in its terminal |

## 💳 Payment Workflow

1. 🏢 Register or sign in to an organizer account.
2. ➕ Create an event and provide the organizer's UPI ID along with the event details.
3. 🎫 A customer selects an event and ticket quantity and creates a booking.
4. 📱 EventSphere displays a UPI QR code for the exact booking amount and a limited payment window.
5. 💸 The customer completes payment in their UPI application and submits the transaction reference (UTR) in EventSphere.
6. 🔎 The organizer checks their bank or UPI account and approves or rejects the payment request.
7. ✅ Once approved, the customer can open **My Bookings** and download the ticket with its verification QR code.

#### Payment PDF
[EventSphere ticket.pdf](https://github.com/user-attachments/files/35209404/EventSphere.ticket.pdf)

## 🔧 Environment Configuration

The backend configuration is in `server/.env.example`. It includes:

- 🔐 `SECRET_KEY` and `JWT_SECRET` for application security and token signing.
- 🗄️ `DATABASE_URL` for the database connection (SQLite is the default).
- 🌐 `CLIENT_ORIGIN` for the frontend origin.
- 💳 Optional Razorpay configuration variables for payment-related integration.

The frontend configuration is in `client/.env.example` and contains `VITE_API_URL`, which points to the backend API.

⚠️ Do not commit real `.env` files, passwords, API keys, or other secrets to a public repository. Use strong, unique secret values before deployment.

## 🔮 Future Improvements

The following features are planned for future development:

- 🛡️ **Admin Dashboard:** A centralized dashboard for administrators to manage customers, organizers, events, bookings, and platform activities.
- ✅ **Event Approval System:** Allow administrators to review and approve events before publication.
- 📈 **Advanced Analytics:** Display platform statistics, booking trends, revenue reports, and user activity.
- 💳 **Automated Payment Verification:** Integrate a payment gateway to automatically verify transactions and payment status.
- 🔔 **Enhanced Notifications:** Send automated email and in-app notifications for booking confirmations, payment updates, and event reminders.
- 🔍 **Advanced Search and Filters:** Improve event discovery with location-based search, categories, dates, and personalized recommendations.

## ⚠️ Important Notes

- Currently, EventSphere provides two dashboards: **Customer Dashboard** and **Organizer Dashboard**.
- The Admin Dashboard is a planned future enhancement and is not currently implemented.
- The current UPI workflow uses **manual organizer approval**. It does not automatically verify payments with a bank or UPI provider.
- Organizers must confirm that the payment has actually arrived in their account before approving a UTR. A submitted reference or screenshot alone is not proof of payment.
- UPI QR-code behavior may vary between devices and UPI applications.
- Use test data during development. Review security, payment verification, and deployment configuration before making the application publicly available.

## 🧪 Local Development

To create a production frontend build, run the following from the `client` folder:

```bash
npm run build
```

To check that the backend is responding, open:

```text
http://127.0.0.1:5000/api/health
```

---
### Author
Shikha Patel - B.Tech(CS)

### 🌟 EventSphere — Find your moment. Book your experience.
