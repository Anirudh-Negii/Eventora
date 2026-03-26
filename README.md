# Eventora

Eventora is a full-stack MERN (MongoDB, Express.js, React, Node.js) event booking platform with OTP-based verification, role-based dashboards, and admin-managed booking confirmations.

## 📌 Project Overview

Eventora enables users to discover events, request bookings, and track booking status from a personal dashboard, while admins can create/manage events and approve booking requests. The platform includes email-based OTP flows for account verification and booking verification, with MongoDB-backed persistence for users, events, OTPs, and bookings.

Screenshots and system documentation (DFD, flowcharts) are available in the `assets/` folder.

## ✨ Features

- User registration and login with JWT authentication.
- Email OTP verification for account activation.
- Event discovery with search and event detail pages.
- OTP-based booking request flow for additional verification.
- User dashboard to view and cancel booking requests.
- Admin dashboard to create/delete events and manage booking approvals.
- Booking states (`pending`, `confirmed`, `cancelled`) and payment states (`paid`, `not_paid`).
- Automated email notifications for OTP and booking confirmations.
- Seed script for quick local data setup.

## 🧰 Tech Stack

- Frontend: React, Vite, Tailwind CSS, React Router, Axios, React Icons.
- Backend: Node.js, Express.js.
- Database: MongoDB with Mongoose.
- Authentication/Security: JWT, bcrypt.
- Email Service: Nodemailer with Gmail SMTP.

## 🏗️ Architecture Overview

1. React frontend (`client`) handles UI, routing, and authenticated API calls.
2. Express backend (`server`) exposes REST endpoints for auth, events, and bookings.
3. JWT middleware protects private/admin routes and enforces role-based access.
4. Business logic in controllers validates OTPs, manages booking lifecycle, and updates seat availability.
5. MongoDB stores application entities (`User`, `Event`, `Booking`, `OTP`).
6. Nodemailer service sends OTP and booking confirmation emails.

High-level flow:

`Frontend (React)` → `REST API (Express)` → `MongoDB (Mongoose)`

`REST API (Express)` → `Email Service (Nodemailer/Gmail SMTP)`

## 🗂️ Project Structure

```text
Eventora/
├── assets/
│   ├── docs/                 # DFD, flowcharts, and supporting documentation
│   └── screenshots/          # UI snapshots
├── client/
│   ├── src/
│   │   ├── components/       # Shared UI components (e.g., Navbar)
│   │   ├── context/          # Auth context and session state
│   │   ├── pages/            # Home, Event Detail, Auth, User/Admin dashboards
│   │   └── utils/axios.js    # Axios instance and auth header interceptor
│   ├── index.html
│   └── package.json
├── server/
│   ├── controllers/          # Route handlers and business logic
│   ├── middleware/           # JWT auth and admin guard middleware
│   ├── models/               # Mongoose models (User, Event, Booking, OTP)
│   ├── routes/               # API route modules (auth, events, bookings)
│   ├── utils/email.js        # Email transport + OTP/booking email helpers
│   ├── seed.js               # Seed script for demo users/events/bookings
│   ├── server.js             # Express app bootstrap + DB connection
│   └── package.json
└── README.md
```

## ⚙️ Environment Setup

Create a `.env` file inside `server/` with:

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
EMAIL_USER=your_gmail_address
EMAIL_PASS=your_gmail_app_password
JWT_SECRET=your_jwt_secret
```

Notes:

- `EMAIL_PASS` should be a Gmail App Password, not your primary account password.
- Keep `.env` values private and never commit them to source control.

## 🚀 Local Development Setup

1. Clone the repository and move into the project root.
2. Install server dependencies:

```bash
cd server
npm install
```

3. Install client dependencies:

```bash
cd ../client
npm install
```

4. Configure environment variables in `server/.env`.
5. Start backend server:

```bash
cd ../server
npm run dev
```

6. Start frontend app in a second terminal:

```bash
cd client
npm run dev
```

7. Open the frontend URL shown by Vite (typically `http://localhost:5173`).

Optional: seed demo data (users/events/bookings):

```bash
cd server
npm run seed
```

## 🔮 Future Improvements

- Integrate a real payment gateway (e.g., Razorpay/Stripe) for end-to-end online checkout.
- Add webhook-based payment verification and automatic payment status reconciliation.
- Move client API base URL to environment variables for multi-environment deployments.
- Add pagination, advanced filtering, and sorting for event discovery.
- Introduce unit/integration tests for controllers and critical user flows.
- Add containerized deployment and CI/CD pipelines for streamlined releases.
