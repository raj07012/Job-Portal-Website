# ⚡ HireHub — Full Stack Job Portal

## Tech Stack
- **Backend:** Node.js + Express + MongoDB Atlas + JWT + Multer
- **Frontend:** React (Vite) + React Router + Axios

---

## 🚀 Setup Instructions

### Step 1: MongoDB Atlas Setup
1. Go to https://cloud.mongodb.com and create a FREE account
2. Create a new **Cluster** (free tier M0)
3. Create a **Database User** (username + password)
4. In **Network Access**, click "Add IP Address" → **Allow Access from Anywhere** (0.0.0.0/0)
5. Click **Connect** → **Drivers** → copy your connection string
   - It looks like: `mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/`

---

### Step 2: Backend Setup

```bash
cd backend
npm install
```

Create `.env` file (copy from `.env.example`):
```
PORT=5000
MONGO_URI=mongodb+srv://YOUR_USERNAME:YOUR_PASSWORD@cluster0.xxxxx.mongodb.net/jobportal?retryWrites=true&w=majority
JWT_SECRET=any_random_long_string_here_keep_it_secret
```

Start backend:
```bash
npm run dev
```
✅ Backend runs at: http://localhost:5000

---

### Step 3: Frontend Setup

```bash
cd frontend
npm install
npm run dev
```
✅ Frontend runs at: http://localhost:5173

---

## 📋 Features

### Job Seeker
- ✅ Register / Login with JWT
- ✅ Browse & Search jobs (filter by type, location, experience)
- ✅ Apply with resume upload + cover letter
- ✅ Track application status (Pending → Shortlisted → Hired)
- ✅ Edit profile, bio, skills, location
- ✅ Upload & save resume

### Recruiter
- ✅ Register / Login as recruiter
- ✅ Post jobs with full details (title, description, skills, salary, type)
- ✅ Edit / Delete / Pause jobs
- ✅ View all applicants per job
- ✅ Update application status (Reviewed / Shortlisted / Rejected / Hired)
- ✅ Recruiter profile management

---

## 📁 Project Structure
```
jobportal/
├── backend/
│   ├── config/db.js          # MongoDB connection
│   ├── controllers/          # Business logic
│   │   ├── authController.js
│   │   ├── jobController.js
│   │   └── applicationController.js
│   ├── middleware/
│   │   ├── auth.js           # JWT + role guards
│   │   └── upload.js         # Multer file upload
│   ├── models/
│   │   ├── User.js
│   │   ├── Job.js
│   │   └── Application.js
│   ├── routes/
│   │   ├── authRoutes.js
│   │   ├── jobRoutes.js
│   │   └── applicationRoutes.js
│   ├── uploads/              # Resume files stored here
│   ├── server.js
│   └── .env                  # ← CREATE THIS FILE
│
└── frontend/
    ├── src/
    │   ├── context/AuthContext.jsx
    │   ├── utils/api.js
    │   ├── components/
    │   │   ├── Navbar.jsx
    │   │   └── PrivateRoute.jsx
    │   ├── pages/
    │   │   ├── Home.jsx
    │   │   ├── Login.jsx
    │   │   ├── Register.jsx
    │   │   ├── Jobs.jsx
    │   │   ├── JobDetail.jsx
    │   │   ├── JobSeekerDashboard.jsx
    │   │   └── RecruiterDashboard.jsx
    │   ├── App.jsx
    │   ├── main.jsx
    │   └── index.css
    └── vite.config.js
```

---

## 🔑 API Endpoints

| Method | Endpoint | Access |
|--------|----------|--------|
| POST | /api/auth/register | Public |
| POST | /api/auth/login | Public |
| GET | /api/auth/me | Private |
| PUT | /api/auth/profile | Private |
| GET | /api/jobs | Public |
| GET | /api/jobs/:id | Public |
| POST | /api/jobs | Recruiter |
| PUT | /api/jobs/:id | Recruiter |
| DELETE | /api/jobs/:id | Recruiter |
| GET | /api/jobs/recruiter/my | Recruiter |
| POST | /api/applications/:jobId | Job Seeker |
| GET | /api/applications/my | Job Seeker |
| GET | /api/applications/recruiter/all | Recruiter |
| GET | /api/applications/job/:jobId | Recruiter |
| PUT | /api/applications/:id/status | Recruiter |
