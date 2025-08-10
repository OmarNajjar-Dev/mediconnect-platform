# MediConnect - Modern Healthcare Connection Platform

<div align="center">
  <h3>🏥 Connecting Patients with Healthcare Professionals</h3>
  <p>A modern, full‑stack healthcare platform powered by Next.js, TypeScript, shadcn/ui, Jest, Laravel, and PostgreSQL</p>
  
  <p>
    <img src="https://img.shields.io/badge/Next.js-000000?style=flat&logo=next.js&logoColor=white" alt="Next.js" />
    <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white" alt="TypeScript" />
    <img src="https://img.shields.io/badge/shadcn%2Fui-111827?style=flat" alt="shadcn/ui" />
    <img src="https://img.shields.io/badge/Jest-C21325?style=flat&logo=jest&logoColor=white" alt="Jest" />
    <img src="https://img.shields.io/badge/Laravel-FF2D20?style=flat&logo=laravel&logoColor=white" alt="Laravel" />
    <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white" alt="PostgreSQL" />
  </p>
</div>

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [User Roles & Permissions](#user-roles--permissions)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Design System](#design-system)
- [Security](#security)
- [Contributing](#contributing)
- [License](#license)

## 🌟 Overview

MediConnect is a comprehensive healthcare web platform designed to bridge the gap between patients and healthcare providers. It is delivered as a monorepo with a modern frontend built on Next.js and TypeScript, and a robust backend powered by Laravel with PostgreSQL.

### Why MediConnect?

- **🚀 Lightning Fast**: Optimized Next.js app with modern tooling
- **♿ Accessible**: WCAG-compliant design ensures universal access
- **📱 Responsive**: Seamless experience across all devices
- **🔒 Secure**: Role-based access control and input validation
- **🌍 Scalable**: Clean architecture ready for growth

## ✨ Key Features

### For Patients

- **🔍 Doctor Discovery**

  - Browse verified healthcare professionals
  - Filter by specialty, location, and ratings
  - View detailed profiles and qualifications

- **🏥 Hospital Directory**

  - Comprehensive listing of healthcare facilities
  - Real-time availability status
  - Distance-based search results

- **📅 Smart Appointment Booking**

  - Schedule appointments with ease
  - Receive confirmation notifications
  - Manage upcoming and past appointments

- **🚨 Emergency Services**
  - Quick access to emergency care
  - COVID-19 focused response system
  - Real-time ambulance tracking

### For Healthcare Providers

- **📊 Role-Based Dashboards**

  - Customized interfaces for each user type
  - Real-time analytics and insights
  - Streamlined workflow management

- **👥 Patient Management**

  - Digital patient records
  - Appointment scheduling tools
  - Prescription management system

- **🔐 Access Control**
  - Granular permission settings
  - Secure data handling
  - Audit trail functionality

### Platform Features

- **⭐ Rating & Review System**: Build trust through patient feedback
- **🔄 Live Updates**: Real-time status tracking for appointments
- **🌐 Multi-language Support**: Reaching a global audience
- **📱 Progressive Enhancement**: Works on any device, any connection

## 👥 User Roles & Permissions

| Role               | Access Level          | Key Capabilities                                                                   |
| ------------------ | --------------------- | ---------------------------------------------------------------------------------- |
| **Super Admin**    | Full Platform Control | • Complete system management<br>• User role assignment<br>• Platform configuration |
| **Admin**          | Hospital Management   | • Doctor management<br>• Appointment oversight<br>• Facility settings              |
| **Doctor**         | Medical Services      | • Patient record access<br>• Prescription management<br>• Schedule control         |
| **Patient**        | Personal Health       | • Appointment booking<br>• Medical history access<br>• Profile management          |
| **Ambulance Team** | Emergency Response    | • Real-time dispatch<br>• Route optimization<br>• Patient status updates           |

## 🛠 Tech Stack

### Frontend

- **Next.js (App Router)** — React framework for SSR/SSG and routing
- **TypeScript** — Type‑safe development
- **shadcn/ui** — Accessible, composable UI primitives
- **Jest** — Unit testing framework

### Backend

- **Laravel (PHP)** — API, business logic, and authentication
- **PostgreSQL** — Primary relational database

### Architecture

- **Monorepo** — Frontend (`frontend-next`) and backend (`backend-laravel`) in a single repository
- **RESTful API** — Clean separation between client and server
- **Modular Components** — Reusable UI elements and services

## 📁 Monorepo Structure

```
mediconnect-platform/
├─ README.md                     # Root, executable overview (this file)
├─ frontend-next/                # Next.js + TypeScript + shadcn/ui + Jest
│  └─ README.md                  # Detailed frontend guide
└─ backend-laravel/              # Laravel + PostgreSQL
   └─ README.md                  # Detailed backend guide
```

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ and npm (or pnpm/yarn)
- PHP 8.2+ and Composer
- PostgreSQL 13+

### 1) Clone

```bash
git clone https://github.com/OmarNajjar-Dev/mediconnect-platform.git
cd mediconnect-platform
```

### 2) Frontend setup (`frontend-next`)

```bash
cd frontend-next
npm install
npm run dev
# App runs at http://localhost:3000
```

### 3) Backend setup (`backend-laravel`)

```bash
cd backend-laravel
cp .env.example .env
composer install
php artisan key:generate

# Configure PostgreSQL in .env
# DB_CONNECTION=pgsql
# DB_HOST=127.0.0.1
# DB_PORT=5432
# DB_DATABASE=mediconnect
# DB_USERNAME=postgres
# DB_PASSWORD=your_password

php artisan migrate
php artisan serve
# API runs at http://localhost:8000
```

### 4) Testing

- Frontend (Jest):
  ```bash
  cd frontend-next
  npm test
  ```
- Backend (PHPUnit):
  ```bash
  cd backend-laravel
  php artisan test
  ```

## 🎨 Design System

### Color Palette

```css
:root {
  /* Brand Colors */
  --primary: 0, 150, 136; /* Medical Teal */
  --primary-light: 178, 223, 219; /* Light Teal */
  --primary-dark: 0, 105, 92; /* Dark Teal */

  /* Semantic Colors */
  --success: 34, 197, 94; /* Green */
  --danger: 239, 68, 68; /* Red */
  --warning: 249, 115, 22; /* Orange */
  --info: 59, 130, 246; /* Blue */

  /* Neutral Palette */
  --neutral-50: 249, 250, 251; /* Lightest */
  --neutral-900: 17, 24, 39; /* Darkest */
}
```

### Typography

- **Headings**: System UI stack for optimal readability
- **Body**: Inter, system-ui, sans-serif
- **Code**: 'Fira Code', monospace

### Components (shadcn/ui)

- **Cards**: Elevation and motion applied via utility classes
- **Buttons**: Variants (primary, secondary, ghost) using design tokens
- **Forms**: Accessible with labels, validation, and error states
- **Tables**: Responsive with horizontal scroll on mobile
- **Modals/Dialogs**: Accessible overlays with focus management

### Responsive Breakpoints

```css
/* Mobile First Approach */
@media (min-width: 640px) {
  /* Tablet */
}
@media (min-width: 1024px) {
  /* Desktop */
}
@media (min-width: 1280px) {
  /* Wide */
}
```

## 🔒 Security

### Implementation

- **Input Validation**: Client and server-side validation
- **SQL Injection Prevention**: Prepared statements
- **XSS Protection**: Output encoding and CSP headers
- **CSRF Protection**: Token-based form submissions
- **Session Security**: Secure session handling

### Best Practices

- Regular security audits
- Dependency updates
- Secure password hashing (bcrypt)
- HTTPS enforcement in production

## 🤝 Contributing

We welcome contributions from the community! Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting a PR.

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Code Style

- **Backend**: PSR-12 (PHP/Laravel)
- **Frontend**: ESLint + Prettier (TypeScript/React)
- Maintain consistent indentation (2 spaces)
- Write meaningful commit messages

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">
  <p>Built with ❤️ by the MediConnect Team</p>
  <p>
    <a href="https://github.com/OmarNajjar-Dev/MediConnect">GitHub</a> •
    <a href="#contributing">Contribute</a> •
    <a href="#license">License</a>
  </p>
</div>
