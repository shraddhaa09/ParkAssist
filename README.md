# ParkAssist

> **Configurable Operator-Assisted Parking Management and Preference-Aware Slot Allocation Platform**

Academic Web Technologies project for VIT Pune (**CS3111::Web Technologies**).

---

## 1. Overview & Core Product Philosophy

ParkAssist is a configurable web-based parking management platform designed for operators (Admins, Entry Staff, and Exit Staff) rather than direct customer self-service. The core workflow follows:

$$\text{System Recommends} \longrightarrow \text{Staff Reviews/Confirms} \longrightarrow \text{System Records Transaction}$$

### Key Capabilities
- **Multi-Model Parking**: Supports both **Slot-Based** (discrete spaces like `A01`, `B27`) and **Capacity-Based** (open areas tracking max, current, and available capacity).
- **Preference-Aware Explainable Allocation Engine**: Deterministic recommendation based on vehicle category (`TWO_WHEELER`, `FOUR_WHEELER`, `COMMERCIAL`), EV requirements (`electric = true/false`), requested features (e.g. `Near Elevator`, `Covered`), and pricing models.
- **Manual Staff Override**: Operators can manually choose any valid compatible space, and every override is logged to the server-side audit trail.
- **Temporary Hold & Expiry**: Concurrency-safe reservation holds with countdown timers to prevent double-booking.
- **Interactive Parking Map**: BookMyShow-style visual slot grid with intuitive operational status colors (Available, Occupied, Held, Blocked, Recommended).
- **Flexible Pricing Strategies**: Strategy pattern implementation supporting `FLAT`, `HOURLY`, `DAILY`, and `SLAB` duration tiers, with `PAY_AT_ENTRY` and `PAY_AT_EXIT` workflows.
- **Role-Based Access Control & Strict Facility Isolation**: JWT authentication with Spring Security method-level guards (`ADMIN`, `STAFF_ENTRY`, `STAFF_EXIT`), ensuring complete data isolation between parking facilities.
- **Multilingual UI**: Instant language switching across **English**, **हिन्दी (Hindi)**, and **मराठी (Marathi)**.

---

## 2. Tech Stack

### Backend
- **Framework**: Spring Boot (Java 26 / Target 25)
- **Database**: PostgreSQL with Hibernate / Spring Data JPA
- **Security**: Spring Security 6 with Stateless JWT Bearer tokens
- **Architecture**: Modular Monolith (Package-by-Feature)
- **API Documentation**: OpenAPI 3.0 / Swagger UI (`/swagger-ui/index.html`)

### Frontend
- **Framework**: React 18 + TypeScript + Vite
- **Styling**: Tailwind CSS with responsive layout & `@media print` ticket support
- **Icons**: Lucide React
- **HTTP Client**: Axios with JWT interceptor and unified error normalization
- **i18n**: Custom multilingual translation dictionary (English, Hindi, Marathi)

---

## 3. Getting Started

### Prerequisites
- Java 25 or higher
- PostgreSQL 16+ running on `localhost:5432` with database `parkassist`
- Node.js (v20+ or v22+) & npm

### Backend Setup
```powershell
cd backend
# Set your PostgreSQL password environment variable (or configure application.properties)
$env:PARKASSIST_DB_PASSWORD="your_postgres_password"
.\mvnw.cmd spring-boot:run
```
The backend starts at `http://localhost:8080`.
- Swagger UI: `http://localhost:8080/swagger-ui/index.html`
- OpenAPI Docs: `http://localhost:8080/v3/api-docs`

### Frontend Setup
```powershell
cd frontend
npm install
npm run dev
```
The frontend dev server starts at `http://localhost:5173` with automatic API proxy to `http://localhost:8080`.

---

## 4. Default & Test Credentials

| Role | Username | Password |
| :--- | :--- | :--- |
| **Admin** | `admin_manual_001` | `Admin@12345` |
| **Entry Staff** | `entry_staff_001` | `Staff@12345` |
| **Exit Staff** | `exit_staff_001` | `Staff@12345` |

*(Quick test buttons are built into the Login Page for fast operator role switching during demonstrations.)*

---

## 5. Verification & Testing

### Run Backend Test Suite
```powershell
cd backend
.\mvnw.cmd test
```
Runs all 21 automated integration and unit test scenarios, including:
- End-to-end Onboarding -> Slot -> Allocation -> Hold -> Session -> Exit -> Payment -> Report flow
- Concurrency test (preventing race conditions when multiple threads request the same slot)
- Capacity overflow prevention
- Manual override audit log generation
- RBAC authorization enforcement
- Multi-facility data isolation

### Run Frontend Build Verification
```powershell
cd frontend
npm run build
```
Executes TypeScript type-checking (`tsc -b`) and Vite production bundling.
"# ParkAssist" 
