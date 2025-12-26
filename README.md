# Multi-Tenant SaaS Project Management System

A fully containerized, production-ready Multi-Tenant SaaS application built with **Node.js**, **React**, and **PostgreSQL**. This system features strict data isolation, Role-Based Access Control (RBAC), and a responsive dashboard for managing projects and tasks.

## 🚀 Quick Start (One-Command Deployment)

Per the submission requirements, this application is fully dockerized and requires **Docker Desktop** to run.

### Prerequisites
* **Docker Desktop** (running)
* **Git**

### Installation & Execution
1.  **Clone the Repository**
    ```bash
    git clone <your-repo-url>
    cd multi-tenant-saas
    ```

2.  **Run the Application**
    Execute the following command in the root directory. This will build the containers, initialize the database, run migrations, and seed default data automatically.
    ```bash
    docker-compose up -d
    ```

3.  **Access the Application**
    * **Frontend (UI):** [http://localhost:3000](http://localhost:3000)
    * **Backend API:** [http://localhost:5000](http://localhost:5000)
    * **Health Check:** [http://localhost:5000/api/health](http://localhost:5000/api/health)

---

## 🔑 Test Credentials (Seed Data)

The system automatically loads the following accounts on startup. Use these to test different roles.

### 1. Super Admin (System Owner)
* **Login URL:** [http://localhost:3000/login](http://localhost:3000/login) (Leave "Organization Subdomain" empty)
* **Email:** `superadmin@system.com`
* **Password:** `Admin@123`
* **Access:** View all tenants, manage system settings.

### 2. Tenant Admin (Organization Manager)
* **Login URL:** [http://localhost:3000/login](http://localhost:3000/login)
* **Subdomain:** `demo`
* **Email:** `admin@demo.com`
* **Password:** `Demo@123`
* **Access:** Manage projects, tasks, and users within the "Demo Company".

### 3. Regular User (Employee)
* **Login URL:** [http://localhost:3000/login](http://localhost:3000/login)
* **Subdomain:** `demo`
* **Email:** `user1@demo.com`
* **Password:** `User@123`
* **Access:** View assigned tasks, view projects.

---

## 📚 Documentation

Detailed documentation regarding the design and architecture of this system can be found in the `docs/` folder:

* **[Research & Analysis](docs/research.md):** Technology stack justification, multi-tenancy analysis, and security considerations.
* **[Product Requirements (PRD)](docs/PRD.md):** User personas, functional/non-functional requirements.
* **[System Architecture](docs/architecture.md):** High-level system design, database ERD, and component breakdown.
* **[Technical Specification](docs/technical-spec.md):** Detailed folder structure, development setup, and testing guide.
* **[API Documentation](docs/api.md):** Full list of the 19 RESTful API endpoints.

---

## 🏗 System Architecture

The application follows a **3-Tier Architecture** wrapped in Docker containers:

1.  **Frontend:** React.js (SPA) with Tailwind CSS.
2.  **Backend:** Node.js / Express.js REST API.
3.  **Database:** PostgreSQL (v15) with `pgcrypto` for password hashing.

### Key Features
* **Multi-Tenancy:** Row-level isolation using `tenant_id`.
* **Authentication:** JWT-based stateless authentication.
* **RBAC:** Granular permissions for Super Admins, Tenant Admins, and Users.
* **Audit Logging:** Tracks critical actions (Create User, Delete Project) for security.
* **Mobile Friendly:** Responsive dashboard with sidebar navigation.

---

## 📂 Project Structure

```text
multi-tenant-saas/
├── docker-compose.yml       # Orchestration for DB, Backend, Frontend
├── submission.json          # Credentials for automated evaluation
├── backend/                 # Node.js API
│   ├── src/controllers/     # Business Logic
│   ├── src/routes/          # API Endpoints
│   ├── migrations/          # SQL Schema definitions
│   └── seeds/               # Initial Data (SQL)
├── frontend/                # React Application
│   ├── src/pages/           # Dashboard, Login, Projects
│   └── src/components/      # Reusable UI (Layout, Navbar)
└── docs/                    # Architectural & Research documentation

---

## 🛠 Development Commands
If you need to rebuild the containers after making code changes:

Rebuild only the backend
docker-compose up -d --build backend

Rebuild only the frontend
docker-compose up -d --build frontend

Stop all services and remove volumes (Reset Database)
docker-compose down -v