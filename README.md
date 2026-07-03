# 🏥 Healthcare Appointment & Follow-up Manager

**An AI-powered healthcare appointment and follow-up management platform built with Java, Spring Boot, React, and PostgreSQL.**

A full-stack clinic management application with dedicated portals for patients, doctors, and administrators. The platform supports appointment scheduling, AI-generated visit summaries, email notifications, and Google Calendar integration.

## 🛠️ Technologies & Skills

### Backend & Database

![Java](https://img.shields.io/badge/Java_17-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white)
![Spring Data JPA](https://img.shields.io/badge/Spring_Data_JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white)
![Maven](https://img.shields.io/badge/Apache_Maven-C71A36?style=for-the-badge&logo=apachemaven&logoColor=white)

### Frontend

![React](https://img.shields.io/badge/React_18-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![Axios](https://img.shields.io/badge/Axios-5A29E4?style=for-the-badge&logo=axios&logoColor=white)

### AI & Integrations

![Groq](https://img.shields.io/badge/Groq_AI-F55036?style=for-the-badge)
![Llama](https://img.shields.io/badge/Llama_3.3-0467DF?style=for-the-badge&logo=meta&logoColor=white)
![Google Calendar](https://img.shields.io/badge/Google_Calendar-4285F4?style=for-the-badge&logo=googlecalendar&logoColor=white)
![OAuth 2.0](https://img.shields.io/badge/OAuth_2.0-3B82F6?style=for-the-badge)
![Brevo](https://img.shields.io/badge/Brevo_Email-0B996E?style=for-the-badge)
![REST API](https://img.shields.io/badge/REST_API-009688?style=for-the-badge)

---

## 📌 Project Overview

The **Healthcare Appointment & Follow-up Manager** is a full-stack healthcare application designed to simplify appointment scheduling, improve communication, and help doctors prepare for patient visits.

The application provides three dedicated user experiences:

- **Patients:** Book appointments, submit symptoms, view appointment information, and receive follow-up communication.
- **Doctors:** Review appointments, access AI-generated pre-visit summaries, record consultation notes, and manage prescriptions.
- **Administrators:** Manage doctor profiles, availability, and scheduling information.

The system integrates the Groq API for AI-generated summaries, Brevo for email notifications, and Google Calendar for appointment events.

## ✨ Key Features

### 👤 Patient Portal

- Patient registration and login
- JWT-based authentication
- Doctor search by specialization
- Appointment availability lookup
- Appointment booking and cancellation
- Symptom submission before appointments
- Appointment confirmations and reminders
- Post-visit summary access

### 👨‍⚕️ Doctor Portal

- View scheduled appointments
- Review patient-submitted symptoms
- Access AI-generated pre-visit summaries
- Submit consultation notes
- Generate patient-friendly post-visit summaries
- Add prescriptions
- Manage appointment-related information

### 🛡️ Administrator Portal

- Create doctor profiles
- Manage doctor specializations
- Configure working hours
- Set appointment slot durations
- Manage doctor leave days

### 🤖 AI-Powered Visit Summaries

The application uses the Groq API with the `llama-3.3-70b-versatile` model.

**Pre-Visit Summary**

Generated when a patient books an appointment and submits symptoms.

The summary includes:

- Suggested urgency level
- Chief complaint
- Questions the doctor may want to ask

**Post-Visit Summary**

Generated from doctor-submitted notes.

The summary is designed to explain:

- Diagnosis information
- Medication instructions
- Lifestyle advice
- Follow-up recommendations

AI-generated information is intended to assist communication and clinical review. It should not replace professional medical judgment.

### 📅 Google Calendar Integration

The application integrates with Google Calendar API v3 using OAuth 2.0.

Calendar integration supports appointment event creation and scheduling coordination.

### 📧 Email Notifications

Brevo REST API integration supports appointment-related emails and patient communication.

### 🚫 Double-Booking Prevention

A PostgreSQL partial unique index prevents multiple active appointments from occupying the same doctor, date, and time slot.

---

## 🏗️ System Architecture

The application uses a React frontend connected to a Spring Boot REST API.

**Frontend**

- React 18
- Vite
- Axios

**Backend**

- Java 17
- Spring Boot 4.1.0
- Spring Security
- Spring Data JPA

**Database**

- PostgreSQL 18

**External Integrations**

- Groq AI API
- Brevo Email API
- Google Calendar API

### Application Workflow

1. A patient registers or logs in.
2. The patient searches for a doctor and available appointment slots.
3. The patient selects a date and time and submits symptoms.
4. The backend validates the booking.
5. The AI service generates a pre-visit summary.
6. The system creates appointment-related email and calendar events.
7. The doctor reviews the appointment and submits consultation notes.
8. The AI service generates a patient-friendly post-visit summary.

---

## 📁 Project Structure

```text
care/
├── health/
│   └── src/main/java/
│       └── <application-package>/
│           ├── config/
│           ├── controller/
│           ├── dto/
│           │   └── groq/
│           ├── entity/
│           ├── repository/
│           └── service/
│
└── frontend/
    └── src/
        ├── pages/
        │   ├── Login
        │   ├── Register
        │   ├── PatientDashboard
        │   ├── DoctorDashboard
        │   └── AdminDashboard
        └── services/
```

Replace `<application-package>` with the actual package directory used in your source code.

## ⚙️ Prerequisites

Before running the application, install:

- Java 17 or newer
- Maven 3.8+
- PostgreSQL 18
- Node.js 22+
- npm

You will also need:

- Groq API key
- Brevo API key
- Google Cloud project with Google Calendar API enabled
- Google OAuth 2.0 credentials

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd care
```

Replace the placeholder with your published repository URL.

### 2. Configure PostgreSQL

Create the database:

```sql
CREATE DATABASE healthdb;
```

After Hibernate creates the application tables, create the appointment uniqueness index:

```sql
CREATE UNIQUE INDEX uq_doctor_slot_active
ON appointment (
    doctor_id,
    appointment_date,
    appointment_time
)
WHERE status <> 'CANCELLED';
```

This prevents two non-cancelled appointments from using the same doctor and time slot.

Update the appointment text columns if needed:

```sql
ALTER TABLE appointment
ALTER COLUMN pre_visit_summary TYPE TEXT,
ALTER COLUMN post_visit_summary TYPE TEXT,
ALTER COLUMN symptoms TYPE TEXT,
ALTER COLUMN doctor_notes TYPE TEXT;
```

### 3. Configure Backend Properties

Create or update:

`health/src/main/resources/application.properties`

Example configuration:

```properties
# Database
spring.datasource.url=jdbc:postgresql://localhost:5432/healthdb
spring.datasource.username=postgres
spring.datasource.password=${DB_PASSWORD}

# JPA
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

# Server
server.port=8081

# Groq AI
groq.api.key=${GROQ_API_KEY}
groq.api.url=https://api.groq.com/openai/v1/chat/completions
groq.model=llama-3.3-70b-versatile

# Brevo Email
brevo.api.key=${BREVO_API_KEY}
brevo.from.email=${BREVO_FROM_EMAIL}
brevo.from.name=Healthcare App

# Google Calendar
google.calendar.credentials.path=src/main/resources/credentials.json
google.calendar.tokens.path=tokens
```

Set the referenced environment variables before starting the backend.

Do not commit actual passwords, API keys, or OAuth credentials.

### 4. Configure Google Calendar

1. Open Google Cloud Console.
2. Create a Google Cloud project.
3. Enable Google Calendar API.
4. Create OAuth 2.0 credentials.
5. Select the appropriate OAuth application type.
6. Configure the redirect URI expected by your application:

`http://localhost:8888/Callback`

7. Download the OAuth credentials JSON file.
8. Save it as `credentials.json` in the location expected by your backend.
9. Add your Google account as a test user if the OAuth application is in testing mode.
10. Complete authorization when the application requests it.

OAuth tokens are stored in the configured `tokens/` directory.

**Security:** Keep `credentials.json` and the `tokens/` directory out of version control.

### 5. Run the Backend

```bash
cd health
./mvnw spring-boot:run
```

On Windows:

```powershell
cd health
.\mvnw.cmd spring-boot:run
```

Backend URL:

`http://localhost:8081`

### 6. Run the Frontend

Open a second terminal:

```bash
cd frontend
npm install
npm run dev
```

Frontend URL:

`http://localhost:5173`

---

## 🔌 REST API Documentation

### Authentication

| Method | Endpoint | Description | Authentication |
|---|---|---|---|
| POST | `/api/auth/register` | Register a user | Public |
| POST | `/api/auth/login` | Log in and receive JWT | Public |

**Register Request**

```json
{
  "name": "Sample Patient",
  "email": "patient@example.com",
  "password": "example-password",
  "role": "PATIENT"
}
```

**Login Request**

```json
{
  "email": "patient@example.com",
  "password": "example-password"
}
```

**Login Response**

```json
{
  "token": "<JWT_TOKEN>"
}
```

Protected endpoints require:

`Authorization: Bearer <JWT_TOKEN>`

### Doctor Management

| Method | Endpoint | Description | Role |
|---|---|---|---|
| POST | `/api/admin/doctors` | Create doctor profile | ADMIN |
| GET | `/api/doctors?specialization=` | Search doctors | As configured |
| GET | `/api/doctors/{id}/slots?date=` | Available appointment slots | As configured |
| POST | `/api/admin/doctors/{id}/leave` | Mark doctor leave day | ADMIN |

**Create Doctor Request**

```json
{
  "user": {
    "id": 2
  },
  "specialization": "Cardiology",
  "workingHoursStart": "09:00",
  "workingHoursEnd": "17:00",
  "slotDurationMinutes": 30,
  "leaveDays": []
}
```

### Appointment Management

| Method | Endpoint | Description | Role |
|---|---|---|---|
| POST | `/api/appointments/book` | Book appointment | PATIENT |
| GET | `/api/appointments/patient/{id}` | Patient appointments | PATIENT |
| GET | `/api/appointments/doctor/{id}` | Doctor appointments | DOCTOR |
| PUT | `/api/appointments/{id}/cancel` | Cancel appointment | Authorized user |
| PUT | `/api/appointments/{id}/notes` | Submit doctor notes | DOCTOR |
| POST | `/api/appointments/{id}/prescription` | Add prescription | DOCTOR |

**Book Appointment Request**

```json
{
  "patient": {
    "id": 1
  },
  "doctor": {
    "id": 1
  },
  "appointmentDate": "2026-07-10",
  "appointmentTime": "09:00",
  "symptoms": "Example symptoms provided by the patient"
}
```

**Example Response**

```json
{
  "id": 1,
  "appointmentDate": "2026-07-10",
  "appointmentTime": "09:00:00",
  "status": "CONFIRMED",
  "symptoms": "Example symptoms provided by the patient",
  "preVisitSummary": "AI-generated pre-visit summary",
  "calendarEventId": "example-calendar-event-id"
}
```

---

## 🗄️ Database Schema

### Users

```text
users
├── id
├── name
├── email
├── password
└── role
```

Roles:

- PATIENT
- DOCTOR
- ADMIN

Passwords are described as BCrypt-hashed in the project documentation.

### Doctors

```text
doctor
├── id
├── user_id
├── specialization
├── working_hours_start
├── working_hours_end
└── slot_duration_minutes
```

### Doctor Leave Days

```text
doctor_leave_days
├── doctor_id
└── leave_days
```

### Appointments

```text
appointment
├── id
├── patient_id
├── doctor_id
├── appointment_date
├── appointment_time
├── status
├── symptoms
├── doctor_notes
├── pre_visit_summary
├── post_visit_summary
└── calendar_event_id
```

### Prescriptions

```text
prescription
├── id
├── appointment_id
├── medication_name
├── frequency_per_day
├── duration_days
└── instructions
```

## 🤖 AI Integration

### Pre-Visit Summary

The application sends patient-provided symptoms to the Groq API.

The prompt requests:

1. Urgency level
2. Chief complaint
3. Three suggested questions for the doctor

### Post-Visit Summary

The application sends doctor-submitted notes to the Groq API.

The prompt requests:

1. Diagnosis explanation
2. Medication schedule
3. Lifestyle advice
4. Follow-up instructions

### Error Handling

If the Groq service is unavailable, the documented implementation stores a fallback message instead of interrupting the appointment workflow.

Possible fallback messages:

- `Pre-visit summary unavailable`
- `Post-visit summary unavailable`

**Healthcare safety:** AI-generated urgency assessments and summaries should be reviewed by qualified healthcare professionals. The application should not be relied on for emergency triage or independent medical decisions.

## 🔒 Security Considerations

The architecture uses Spring Security and JWT authentication.

For a production healthcare deployment, additional safeguards are important:

- Role-based authorization for patient and doctor records
- Verification that users can access only authorized records
- HTTPS and secure credential storage
- Encryption of sensitive patient information
- Audit logging
- Secure management of OAuth tokens
- Protection of information sent to external AI and email providers
- Healthcare privacy and compliance review

These are production considerations, not claims of regulatory certification.

## ☁️ Deployment

### Backend — Render

The Spring Boot backend can be deployed to a compatible hosting environment such as Render.

Configure the required database, API keys, and OAuth credentials as environment variables or protected secrets.

### Frontend — Vercel

Deploy the React application from the `frontend` directory.

Update the Axios API base URL in:

`frontend/src/services/api.js`

Point it to your deployed backend URL.

Ensure the backend's CORS configuration allows the frontend origin.

### Production Checklist

- Configure a production PostgreSQL database.
- Store credentials securely.
- Configure HTTPS.
- Set the correct frontend API URL.
- Verify OAuth redirect URLs.
- Configure email sender verification.
- Review access controls and data privacy.
- Run tests before deployment.

## 🔮 Future Improvements

- Advanced doctor availability management
- Patient medical history integration
- Appointment reminder scheduling
- Improved AI summary validation
- Audit logs and activity tracking
- Automated integration testing
- CI/CD deployment workflows
- Enhanced analytics for clinic administrators
- Secure patient document management

## 👨‍💻 Contact

**Colby Bean**

Full-Stack Software Engineer

- **Location:** Winter Park, Florida, USA
- **Email:** [colbybean321@gmail.com](mailto:colbybean321@gmail.com)
- **Phone:** +1 (689) 260-2573
- **GitHub:** [github.com/BeanColby44](https://github.com/BeanColby44)
- **LinkedIn:** [linkedin.com/in/colby-bean-922179449](https://www.linkedin.com/in/colby-bean-922179449/)

## 📄 License

Refer to the repository's existing `LICENSE` file for applicable license terms and attribution requirements.