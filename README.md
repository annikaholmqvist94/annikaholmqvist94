# Hi, I'm Annika Holmqvist

**Backend Developer** with a passion for building secure, scalable, and automated software solutions. Currently specializing in Java, Spring Boot, and Cloud Architecture.

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.2-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Railway](https://img.shields.io/badge/Railway-Deployed-black?style=for-the-badge&logo=railway&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-Deployed-000000?style=for-the-badge&logo=vercel&logoColor=white)

---

## Vet1177 – Veterinary Journal System

> A full-stack web application for managing veterinary case records, built as a group project during my Java backend education.

**[Repository](https://github.com/ithsjava25/project-backend-org-random-coders)** · **[Demo video](#)** *(coming soon)*

### What it does
Pet owners can create and track medical cases for their animals, veterinarians manage and respond to cases at their clinic, and admins have full system oversight. The system includes file attachments, a real-time activity log, role-based access control, and a full REST API - all containerized and ready to run with a single command.

### Tech Stack

**Backend**
- **Java 24** · **Spring Boot 4.0.4** (Spring MVC, Spring Data JPA / Hibernate, Spring Security, Spring Validation)
- **OAuth2 Resource Server** – JWT-based stateless authentication
- **PostgreSQL 15** – relational database with UUID primary keys
- **MinIO (S3-compatible)** – object storage for file attachments via **AWS SDK for Java v2**
- **Jackson Databind** – JSON serialization/deserialization
- **SLF4J** – structured application logging
- **JaCoCo** – code coverage reporting
- **Maven** (with Maven Wrapper) – build & dependency management
- **Docker & Docker Compose** – containerized infrastructure (PostgreSQL + MinIO spun up automatically)
- **GitHub Actions** – CI/CD pipeline (automated build & test on every PR)

**Frontend**
- **React 19** + **Vite 8** – modern SPA with fast HMR dev experience
- **Tailwind CSS** – utility-first styling
- **Axios** – HTTP client for REST API communication
- **jwt-decode** – client-side JWT parsing for role-aware UI
- **Lucide React** – icon library
- **ESLint** – code quality enforcement
- **PostCSS / Autoprefixer** – CSS processing pipeline

**Architecture & Practices**
- RESTful API design with a documented `API.md`
- Policy-based authorization layer with per-entity policies custom exceptions mapped to HTTP semantics (400 / 401 / 403 / 404 / 422)
- Global exception handling via `@RestControllerAdvice`
- Activity log / audit trail on all case events
- Environment-variable-driven configuration (`.env.example` included)
- Feature-branch workflow with 150+ branches and 115+ pull requests merged

### Team
Built together with [@lindaeskilsson](https://github.com/lindaeskilsson), [@TatjanaTrajkovic](https://github.com/TatjanaTrajkovic) and [@johanbriger](https://github.com/johanbriger).



## Full-Stack ATS Application

Architecting a professional Applicant Tracking System (ATS) that demonstrates the full lifecycle of modern software development-from secure backend logic to automated cloud deployment and real-time candidate management.

<div align="center">
  <img src="https://github.com/user-attachments/assets/c8ab73c1-be21-46bb-bcab-dec68db06894" width="550" alt="ATS Demo" />
</div>

* **Backend:** Java & Spring Boot with **Supabase JWT Authentication (ES256)** for robust, token-based security.
* **Database:** **Supabase (PostgreSQL)** with Row Level Security and RESTful API integration.
* **DevOps:** Fully automated deployment using **Railway CLI** (backend) and **Vercel** (frontend).
* **Frontend:** Modern, responsive UI built with **React**, **TypeScript**, and **Tailwind CSS** featuring drag-and-drop pipeline management.
* **Key Features:** Candidate management, recruitment pipeline with drag-and-drop stages, detailed scorecards, admin user management, and role-based access control.

**[View Project: mini-ATS (Backend)](https://github.com/annikaholmqvist94/mini-ATS)** | **[View Project: talentflow-pro (Frontend)](https://github.com/annikaholmqvist94/talentflow-pro)** 

🌐 **[Live Demo](https://talentflow-pro.vercel.app)** 

---

## Skills & Tech Stack

| Area | Technologies & Tools |
| :--- | :--- |
| **Language** | Java, TypeScript |
| **Backend** | Spring Boot 3.2, Spring Security, JPA / Hibernate, JWT (ES256) |
| **Databases** | Supabase (PostgreSQL), Azure SQL Database (MSSQL), MySQL |
| **Frontend** | React, TypeScript, Vite, Tailwind CSS, Lovable |
| **DevOps & Cloud** | Railway, Vercel, Azure App Service, GitHub Actions (CI/CD), Docker, Testcontainers |
| **IDE & Environment** | IntelliJ IDEA, macOS / Linux, Git |
| **Practices** | REST API Design, Clean Code, TDD, SOLID Principles |

---

## Featured Projects  

### [TalentFlow Pro - ATS Application (Fullstack)](https://github.com/annikaholmqvist94/mini-ATS)
A cloud-native recruitment management system featuring Supabase authentication, drag-and-drop pipeline management, and automated deployments.
* *Key Tech:* Java 17, Spring Boot, Supabase, Railway, Vercel, React, TypeScript.

### [MeetingApp - Möteshantering (Full-Stack)](https://github.com/annikaholmqvist94/meetingapp)
A professional meeting management application featuring a dark glassmorphism UI, Kanban board with drag-and-drop, dashboard with statistics, and calendar view.
* *Key Tech:* Java 21, Spring Boot, Spring Data JPA, Thymeleaf, PostgreSQL, Docker.

<div align="center">
  <img src="https://github.com/annikaholmqvist94/meetingapp/raw/main/docs/images/dashboard.png" width="550" alt="MeetingApp Dashboard" />
</div>

### [Invoicing Web App (Fullstack)](https://github.com/annikaholmqvist94/invoicing-web-app)
A cloud-native application featuring automated deployments, secure API endpoints, and a professional database setup.
* *Key Tech:* Java 21, Spring Boot, Azure, GitHub Actions.

### [Invoice Management System (Team Project)](https://github.com/ithsjava25/project-jpa-grupp-3-d)
A comprehensive invoice management solution built with clean architecture principles and modern Java practices. This project was a collaborative effort focusing on JPA relationships and system design.

#### Project Collaborators
| Member | Profile |
| :--- | :---: |
| **Annika Holmqvist** | [@annikaholmqvist94](https://github.com/annikaholmqvist94) |
| **Kristina** | [@kristina0x7](https://github.com/kristina0x7) |
| **Fmazmz** | [@fmazmz](https://github.com/fmazmz) |

---

### [TestContainers Integration](https://github.com/ithsjava25/databas-jdbc-annikaholmqvist94/pull/2)
Integration testing at scale. Built a Java CLI with end-to-end tests using **Docker** to run against a temporary MySQL-database.
* *Key Tech:* Java, JDBC, Testcontainers, Docker.

### [CLI & Warehouse Apps](https://github.com/annikaholmqvist94/CLI-app)
Focusing on **Core Java** efficiency, Object-Oriented Design, and **Test Driven Development (TDD)**.

---

## Connect with Me

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Annika%20Holmqvist-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/annika-holmqvist-130911209/)
[![Instagram](https://img.shields.io/badge/Instagram-Reawake%20Estate%20Ltd-pink?style=for-the-badge&logo=instagram)](https://www.instagram.com/reawake_estate_ltd/)
[![Email](https://img.shields.io/badge/Email-annika.holmqvist94@gmail.com-red?style=for-the-badge&logo=gmail)](mailto:annika.holmqvist94@gmail.com)

---

> "Code is like humor. When you have to explain it, it's bad." – Cory House  

Thanks for stopping by — feel free to explore my repositories or reach out for collaborations!
