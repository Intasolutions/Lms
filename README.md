# LMS Academy Platform

A comprehensive, production-ready Learning Management System (LMS) suite consisting of a **Django REST API** backend, a **Next.js (App Router)** responsive web application, and an **Expo (React Native)** mobile app.

---

## 🏛️ System Architecture

```
├── backend/            # Django 6 + Django REST Framework + Celery
│   ├── billing/        # Invoices, subscriptions, recurring cycles
│   ├── cms/            # Dynamic landing page & banner content
│   ├── core/           # Settings, WSGI/ASGI, global JWT middleware
│   ├── courses/        # Course catalog, curriculum, video lectures, live classes
│   ├── finance/        # Teacher payouts, revenue share & financial ledgers
│   ├── notifications/  # In-app notifications & email dispatch
│   ├── orders/         # Razorpay checkout, orders & webhook processing
│   ├── quizzes/        # Assessments, questions & student score tracking
│   └── users/          # Authentication, OTP, OAuth, role profiles
│
├── frontend/           # Next.js 16 (React 19) Web Application
│   ├── src/app/        # App Router pages (Student, Teacher, Admin, Public)
│   ├── src/components/ # Design system components & UI blocks
│   └── src/context/    # Authentication & application state providers
│
└── mobile/             # Expo React Native Mobile App
    └── src/screens/    # Native screens (Home, Learn, Certificates, Profile, etc.)
```

---

## 🚀 Getting Started

### 1. Backend Setup (Django + Celery)

#### Requirements
- Python 3.11 or 3.12
- Redis (optional for local development, required for Celery tasks)
- PostgreSQL (or local SQLite fallback)

#### Installation
```bash
cd backend

# Create and activate virtual environment
python -m venv venv
# On Windows:
venv\Scripts\activate
# On Linux/macOS:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env with your local settings

# Apply database migrations
python manage.py migrate

# Create initial administrator account
python manage.py createsuperuser
# Or run the included script:
python create_admin.py

# Start Django development server
python manage.py runserver 0.0.0.0:8000
```

#### Running Celery (Background Worker & Scheduler)
In separate terminal windows:
```bash
# Celery Worker
celery -A core worker -l info

# Celery Beat (Scheduled Tasks: Invoices, Reminders)
celery -A core beat -l info
```

---

### 2. Frontend Setup (Next.js)

#### Requirements
- Node.js 20+
- npm or yarn

#### Installation
```bash
cd frontend

# Install dependencies
npm install

# Configure environment
cp .env.example .env.local
# Verify NEXT_PUBLIC_API_URL points to http://localhost:8000

# Start development server
npm run dev
```

The frontend will be accessible at `http://localhost:3000`.

---

### 3. Mobile Setup (Expo React Native)

#### Requirements
- Node.js 20+
- Expo Go app on iOS/Android or local simulator

#### Installation
```bash
cd mobile

# Install dependencies
npm install

# Configure environment
cp .env.example .env

# Start Expo dev server
npx expo start
```

Scan the QR code with the Expo Go app or press `a` for Android Emulator / `i` for iOS Simulator.

---

## ⚙️ Key Feature Highlights

- **Course Management:** Multi-tier curriculum with chapters, video lessons, attachments, and progress tracking.
- **Interactive Live Sessions:** Zoom API integration for scheduled webinars and live interactive classes.
- **Certificates & Verification:** Customizable certificates issued upon course completion with unique QR-code verification URLs.
- **Billing & Subscriptions:** Full subscription engine supporting recurring billing cycles, manual/automated invoicing, and Razorpay gateway integration.
- **Teacher Ledger & Payouts:** Automated instructor revenue share calculation and financial ledger tracking.
- **Multi-Role Portal:** Dedicated views and permission controls for Administrators, Instructors, and Students.
- **Cross-Platform:** Consistent user experience across Web (Next.js desktop/mobile responsive) and Native Mobile (iOS & Android).

---

## 🔒 Configuration & Environment Variables

Templates for all environment variables are provided in each component directory:
- [backend/.env.example](backend/.env.example)
- [frontend/.env.example](frontend/.env.example)
- [mobile/.env.example](mobile/.env.example)

---

## 📄 License

Proprietary — Internal product distribution. All rights reserved.
