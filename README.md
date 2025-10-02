# WellSlot — Doctor Appointment Web App

This repository contains a MERN-style doctor appointment application split into three main parts:

- `backend/` — Node.js + Express REST API, MongoDB models, controllers, auth middleware, Cloudinary and Razorpay integrations.
- `frontend/` — Main public React app (Vite) used by patients.
- `admin/` — Admin panel React app (Vite) used to manage doctors and appointments.

This README documents how to run, build, and deploy the project, lists required environment variables, explains authentication headers, and provides quick troubleshooting notes.

## Table of contents

- Project layout
- Quick start (dev)
- Environment variables
- Package scripts
- Ports & URLs
- API overview (endpoints + auth headers)
- Deployment notes
- Troubleshooting & tips

## Project layout

Root structure (important folders):

```
WellSlot/
├── admin/          # Admin React app (vite)
├── backend/        # Express API server (Node.js)
├── frontend/       # Public React app (vite)
└── README.md       # This file
```

Backend highlights:

- Entry: `backend/server.js`
- DB config: `backend/config/mongodb.js` (connects to `${MONGODB_URI}/WellSlot`)
- Cloudinary config: `backend/config/cloudinary.js`
- Routes: `backend/routes/*.js` (admin, doctor, user)
- Controllers: `backend/controllers/*.js`
- Models: `backend/models/*.js`

Frontend highlights:

- `frontend/` is the patient-facing React app (Vite)
- Vite config: `frontend/vite.config.js` (dev server port 5173)
- Entry: `frontend/index.html` -> `/src/main.jsx`

Admin highlights:

- `admin/` is the admin panel React app (Vite)
- Vite config: `admin/vite.config.js` (dev server port 5174)
- Entry: `admin/index.html` -> `/src/main.jsx`

## Quick start (development)

1. Install dependencies for each package (run in separate terminals or run each one sequentially):

```bash
# install backend
cd /WellSlot/backend
npm install

# install frontend
cd /WellSlot/frontend
npm install

# install admin
cd /WellSlot/admin
npm install
```

2. Create a `.env` file inside the `backend/` folder with required variables (see next section).

3. Start the backend and frontends (each in its own terminal):

```bash
# start backend (nodemon recommended for dev)
cd /WellSlot/backend
npm run server

# start patient frontend (Vite)
cd /WellSlot/frontend
npm run dev

# start admin frontend (Vite)
cd /WellSlot/admin
npm run dev
```

4. Open apps in the browser:

- Patient app: http://localhost:5173
- Admin panel: http://localhost:5174
- Backend API: http://localhost:4000 (default)

Note: `PORT` can be set in the backend `.env` to change the backend port.

## Environment variables (backend/.env)

Create `backend/.env` and include the following variables (example placeholders):

```
MONGODB_URI=mongodb+srv://<user>:<pass>@cluster.mongodb.net
JWT_SECRET=super-long-jwt-secret
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=adminpassword
CLOUDINARY_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_key
CLOUDINARY_SECRET_KEY=your_cloudinary_secret
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_secret
CURRENCY=INR
PORT=4000
```


## Package scripts

Backend (`backend/package.json`):

- `npm run server` — starts `nodemon server.js` (recommended for dev)
- `npm start` — runs `node server.js`

Frontend (`frontend/package.json`):

- `npm run dev` — start Vite dev server on port 5173
- `npm run build` — build production `dist`
- `npm run preview` — preview built site

Admin (`admin/package.json`):

- `npm run dev` — start Vite dev server on port 5174
- `npm run build` — build production `dist`

You can also install `concurrently` or similar tools at the repo root to start multiple services together. Example (optional):

```
# Example dev-start helper (not included in repo):
# concurrently "npm:server" "npm:frontend" "npm:admin" --names "BACKEND,FRONT,ADMIN"
```
---

If you'd like, I can create `backend/.env.example`, add a `dev` helper script at the root using `concurrently`, and create a short section in this README with explicit axios/baseURL examples for the frontends. Tell me which of these you'd like me to add and I'll implement them.
# WellSlot - Doctor Appointment Web App

**Appinty** is a full-stack web application designed to make healthcare more accessible by simplifying the process of booking doctor appointments. It offers three levels of login: **Patient**, **Doctor**, and **Admin**, each with distinct features tailored to their roles. The app integrates **online payment gateways (Stripe and Razorpay)** to facilitate seamless and secure payments. Built using the **MERN stack** (MongoDB, Express.js, React.js, and Node.js), WellSlot provides an efficient, user-friendly experience for both patients and healthcare providers.

## 🛠️ Tech Stack

- **Frontend**: React.js
- **Backend**: Node.js, Express.js
- **Database**: MongoDB
- **Payment Gateways**: Razorpay
- **Authentication**: JSON Web Token (JWT)

## 🔑 Key Features

### 1. Three-Level Authentication

- **Patient Login**: 
  - Patients can sign up, log in, and book appointments with doctors.
  - Manage appointments (view, cancel, or reschedule).
  - Secure online payment options available (cash, Stripe, Razorpay).
  - User profile with editable information (name, email, address, gender, birthday, profile picture).

- **Doctor Login**:
  - Doctors can log in and manage appointments.
  - Dashboard displays earnings, number of patients, number of appointments, and latest bookings.
  - Update profile details (description, fees, address, availability status).
  - View appointment details (patient info, payment mode, appointment status).

- **Admin Login**:
  - Admins can create and manage doctor profiles.
  - Dashboard with analytics: total doctors, total appointments, total patients, and recent bookings.
  - Add new doctors (image, specialty, degree, experience, address, fees, etc.).
  - View and manage all appointments (cancel or mark as completed).

## 🏠 Home Page

- Features a user-friendly layout where users can:
  - **Search for doctors** based on specialties.
  - **View top doctors** and their profiles.
  - Explore additional sections: About Us, Delivery Information, Privacy Policy, and Get in Touch.
- **Footer** includes navigation links: Home, About Us, Delivery Info, Privacy Policy, Contact Us.

## 🩺 All Doctors Page

- Lists all available doctors.
- Users can **filter doctors by specialty**.
- Clicking on a doctor's profile redirects to the **Doctor Appointment Page**.

## 📄 About Page

- Provides information about **WellSlot’s vision** and mission.
- **Why Choose Us** section highlights:
  - **Efficiency**: Streamlined appointment process.
  - **Convenience**: Online booking and payment.
  - **Personalization**: Tailored experience based on user preferences.
- Footer section with additional links.

## 📞 Contact Page

- Contains **office address** and contact details.
- Section to explore job opportunities.
- Footer navigation links.

## 📅 Doctor Appointment Page

- Displays detailed information about the selected doctor:
  - **Profile picture, qualification, experience**, and a brief description.
  - **Appointment booking form**: Choose date, time, and payment method.
  - Online payment options: **Cash, Stripe, or Razorpay**.
  - **Related doctors** section at the bottom.
- Users need to **create an account or log in** before booking an appointment.

## 👤 User Profile

- Accessible after login.
- Users can view and edit their profile:
  - **Upload profile picture**.
  - Update **name, email, address, gender, and birthday**.
- View list of upcoming and past appointments.
- **Logout** option available.

## 🗄️ Admin Panel

- **Dashboard**:
  - Displays statistics: **Number of doctors**, **appointments**, **patients**, and **latest bookings**.
  - Option to **cancel bookings** if needed.
- **Add Doctor**:
  - Form to add a new doctor profile (image, specialty, email, password, degree, address, experience, fees, description).
- **Doctor List**:
  - View all registered doctors with options to edit or delete profiles.
- **Appointments**:
  - List of all appointments including patient name, age, date, time, doctor name, fees.
  - Admin actions: **Cancel** or **Mark as Completed**.

## 🩺 Doctor Dashboard

- **Earnings Overview**:
  - Total earnings from completed appointments.
- **Appointments List**:
  - View detailed list of patient appointments (name, age, date, time, payment mode, status).
  - Actions: **Mark appointment as completed** or **Cancel appointment**.
- **Profile Management**:
  - Doctors can update their **profile information**, including description, fees, address, and availability status.

## 💳 Payment Integration

- Supports multiple payment methods:
  - **Cash Payment**
  - **Razorpay Integration**
- Ensures a secure and smooth payment experience for users.

## 🌐 Project Setup

To set up and run this project locally:

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/WellSlot.git
   cd WellSlot
   ```

2. **Install Dependencies**:
   ```bash
   npm install
   cd client
   npm install
   ```

3. **Environment Variables**:
   - Create a `.env` file in the root directory and add the following:
     ```env
     MONGO_URI=your_mongodb_connection_string
     JWT_SECRET=your_jwt_secret
     STRIPE_API_KEY=your_stripe_api_key
     RAZORPAY_API_KEY=your_razorpay_api_key
     ```

4. **Run the Application**:
   ```bash
   npm run dev
   ```

## 📦 Folder Structure

```plaintext
WellSlot/
├── client/          # Frontend (React.js)
├── server/          # Backend (Node.js, Express.js)
├── models/          # MongoDB Schemas
├── controllers/     # API Controllers
├── routes/          # API Routes
├── middleware/      # Authentication and Error Handling
├── config/          # Configuration Files
├── utils/           # Utility Functions
├── public/          # Static Files
└── .env             # Environment Variables
```

## 🤝 Contributing

We welcome contributions! Please feel free to submit issues, fork the repository, and open pull requests.


## 🌟 Acknowledgements

- Thanks to the developers and contributors of MongoDB, Express.js, React.js, Node.js, Stripe, and Razorpay for their fantastic tools and libraries.

---
