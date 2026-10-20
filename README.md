# 🎓 Student Management System (SMS)

A full-stack, responsive academic management platform built with **Laravel 10**, **PHP 8.1+**, and **MySQL**. This application centralizes institutional administration by streamlining record-keeping for students, teachers, academic classes, courses, subjects, and grades—complete with interactive data analytics, bulk Excel import/export, and printable PDF reporting.

---

## 📌 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [System Architecture & Database Schema](#system-architecture--database-schema)
- [Directory Structure](#directory-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation Steps](#installation-steps)
  - [Environment Configuration](#environment-configuration)
- [Module Routes Overview](#module-routes-overview)
- [Contributing](#contributing)
- [License](#license)

---

## 📖 Overview

The **Student Management System** is engineered to eliminate fragmented administrative processes in educational institutions. From enrollment and teacher assignments to subject allocations and report generation, this system provides school administrators with an intuitive, unified dashboard and robust data handling capabilities.

---

## ✨ Key Features

### 📊 1. Centralized Analytics Dashboard
- **Live Metrics**: Displays real-time aggregate statistics for Total Students, Teachers, Courses, Subjects, Classes, and Grades.
- **Modern UI**: Styled with dark glassmorphism cards, gradient accents, and interactive **ApexCharts** data visualizations.

### 👨‍🎓 2. Student Information Management
- **Full CRUD Operations**: Register, view, edit, and delete student records.
- **Document & Image Handling**: Upload and store student profile pictures along with National Identity Card (**NIC Front & Back**) images.
- **Academic Links**: Link students directly to their designated **Grade** and enrolled **Course**.

### 👩‍🏫 3. Teacher Management
- **Faculty Directory**: Manage educator profiles and personal details.
- **Multi-Assignment Support**: Assign teachers to multiple **Subjects** and **Grades** via relational pivot tables.
- **Credential Storage**: Securely upload and manage teacher identification documents.

### 🏫 4. Course, Class, Subject & Grade Modules
- **Course Administration**: Organize study programs and associate them with curriculums.
- **Subject Allocation**: Many-to-many relationship mapping between subjects and courses/teachers.
- **Class & Grade Management**: Structure academic levels and classroom divisions cleanly.

### 📥 5. Bulk Excel Import & Export
- Integrated with `maatwebsite/excel`.
- **Bulk Import**: Quickly upload large spreadsheets (`.xlsx`) to populate students, teachers, grades, subjects, and classes without manual entry.
- **Excel Export**: Download live database tables into spreadsheet format for offline analysis.

### 📄 6. PDF Report Generation
- Powered by `barryvdh/laravel-dompdf`.
- Generates clean, printer-friendly PDF summaries and rosters for any module with a single click.

### 🔐 7. Authentication & Security
- Custom session-based authentication (Registration, Login, Session Regeneration, and Logout).
- Strict password hashing with `bcrypt`.
- Built-in CSRF token protection on all forms.
- Admin profile management view.

### 🎨 8. User Experience & Interface
- Built on **AdminLTE** and **Bootstrap 5**.
- Interactive notifications powered by **SweetAlert2**.
- Fast, searchable multi-select dropdowns using **Tom-Select**.

---

## 🛠️ Technology Stack

| Layer | Technology |
|---|---|
| **Backend Framework** | [Laravel 10.x](https://laravel.com/) |
| **Server Language** | [PHP 8.1+](https://www.php.net/) |
| **Database** | [MySQL](https://www.mysql.com/) (Eloquent ORM) |
| **Frontend & UI** | Blade Templates, [Bootstrap 5](https://getbootstrap.com/), [AdminLTE](https://adminlte.io/) |
| **UI Components** | [SweetAlert2](https://sweetalert2.github.io/), [Tom-Select](https://tom-select.js.org/), [ApexCharts](https://apexcharts.com/) |
| **Document Processing** | [Maatwebsite Excel 3.1](https://laravel-excel.com/), [DOMPDF / Laravel-DomPDF](https://github.com/barryvdh/laravel-dompdf) |
| **Asset Bundler** | [Vite](https://vitejs.dev/) |

---

## 🗄️ System Architecture & Database Schema

The database relies on normalized relational schemas with dedicated pivot tables for many-to-many relationships:

```
[Users]          -> Authentication & administrative accounts
[Students]       -> Belongs to [Grades] and [Courses]
[Teachers]       -> Linked to [Subjects] via `subject_teacher`
                 -> Linked to [Grades] via `grade_teacher`
[Courses]        -> Linked to [Subjects] via `course_subject`
[Classes]        -> Classroom sections
[Grades]         -> Academic grade divisions
```

---

## 📂 Directory Structure

```text
Student_Management_PR01/
├── app/
│   ├── Exports/            # Dedicated Excel export handlers for each model
│   ├── Http/
│   │   └── Controllers/    # Auth, Dashboard, Student, Teacher, Course, etc.
│   ├── Imports/            # Dedicated Excel import handlers for bulk uploads
│   └── Models/             # Eloquent Models (Student, Teacher, Course, etc.)
├── config/                 # Application configuration files
├── database/
│   ├── migrations/         # Schema definitions & pivot tables
│   └── seeders/            # Database seeders
├── public/
│   └── assets/             # AdminLTE styles, custom CSS, JS, and image uploads
├── resources/
│   ├── views/
│   │   ├── auth/           # Login & registration views
│   │   ├── dashboard/      # Analytic dashboard with charts & stat cards
│   │   ├── layouts/        # Base layout master templates
│   │   ├── student/        # Student CRUD views, modal previews, PDF templates
│   │   ├── teacher/        # Teacher CRUD views & assignments
│   │   ├── course/         # Course management views
│   │   ├── subject/        # Subject management views
│   │   ├── class/          # Class management views
│   │   └── grade/          # Grade management views
├── routes/
│   └── web.php             # Web routing & module prefixes
├── .env.example            # Environment template configuration
├── composer.json           # PHP packages & dependencies
└── package.json            # Node/Vite dependencies
```

---

## 🚀 Getting Started

Follow these instructions to set up the project locally on your machine.

### Prerequisites

Ensure you have the following installed on your system:
- **PHP** >= 8.1
- **Composer** >= 2.x
- **Node.js** >= 18.x & **npm**
- **MySQL Server** (via XAMPP, Laragon, Docker, or native service)

---

### Installation Steps

#### 1. Clone the repository
```bash
git clone https://github.com/your-username/student-management-system.git
cd student-management-system
```

#### 2. Install PHP dependencies
```bash
composer install
```

#### 3. Install JavaScript dependencies
```bash
npm install
```

#### 4. Configure environment settings
Copy the sample environment file and adjust your database credentials:
```bash
cp .env.example .env
```

Open `.env` in your code editor and configure your database connection:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=student_management
DB_USERNAME=root
DB_PASSWORD=
```

#### 5. Generate application key
```bash
php artisan key:generate
```

#### 6. Run database migrations
Execute migrations to create all required tables and relationships:
```bash
php artisan migrate
```

*(Optional) Seed initial data if seeders are configured:*
```bash
php artisan db:seed
```

#### 7. Build frontend assets
```bash
# For local development (watches file changes):
npm run dev

# Or compile for production:
npm run build
```

#### 8. Start the local server
```bash
php artisan serve
```

The application will be live at `http://127.0.0.1:8000`.

---

## 🚦 Module Routes Overview

All core modules follow a clean RESTful-style URL pattern grouped with route prefixes:

| Module | Route Prefix | Key Endpoints | Description |
|---|---|---|---|
| **Auth** | `/auth` | `/login`, `/register`, `/logout` | User authentication & session handling |
| **Dashboard** | `/dashboard` | `/` | Metric overview cards and analytics |
| **Students** | `/student` | `/`, `/create`, `/store`, `/edit/{id}`, `/export`, `/import`, `/pdf` | Complete student management & reports |
| **Teachers** | `/teacher` | `/`, `/create`, `/store`, `/edit/{id}`, `/export`, `/import`, `/pdf` | Faculty management, documents & assignments |
| **Courses** | `/course` | `/`, `/create`, `/store`, `/edit/{id}`, `/export`, `/import`, `/pdf` | Course catalogue & records |
| **Subjects** | `/subject` | `/`, `/create`, `/store`, `/edit/{id}`, `/export`, `/import`, `/pdf` | Subject catalogue & allocations |
| **Classes** | `/class` | `/`, `/create`, `/store`, `/edit/{id}`, `/export`, `/import`, `/pdf` | Classrooms & batches |
| **Grades** | `/grade` | `/`, `/create`, `/store`, `/edit/{id}`, `/export`, `/import`, `/pdf` | Grade levels & hierarchies |
| **Profile** | `/profile` | `/` | Authenticated user profile |

---

## 🤝 Contributing

Contributions, issues, and feature suggestions are welcome!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License**.
