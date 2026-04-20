# SEPP-2026 – Shelton Tool-Hire Review Portal System

## 🎓 Overview

The **SEPP-2026 organisation** hosts the development of the **Review Portal System**, an MSc Software Engineering project. The system is designed as a full-stack web application that allows users to submit, view, and manage reviews through a modern interface supported by a backend API.

The project demonstrates practical application of software engineering principles, including modular design, version control, CI/CD automation, and collaborative development.

---

## 🧱 System Structure

The project is organised into two main repositories:

### 🔹 ReviewPortal-Web

Frontend application responsible for:

* User interface and user experience
* Communicating with the backend API
* Handling client-side logic

### 🔹 ReviewPortal-API

Backend service responsible for:

* Business logic
* Data processing and storage
* Providing RESTful API endpoints

This separation allows both components to be developed and deployed independently while maintaining a clear system structure.

---

## ⚙️ Technology Stack

* **Frontend:** TypeScript, NextJS JavaScript framework, HTML, CSS
* **Backend:** .NET (C#), ASP.NET Core Web API
* **DevOps:** GitHub, GitHub Actions, Azure App Service

---

## 🔄 Development Workflow

The project follows a structured Git workflow:

* Feature branches are used for development
* All changes are submitted through pull requests
* Code is reviewed before merging
* The `main` branch is protected

This ensures controlled collaboration and maintains code quality.

---

## 🚀 CI/CD Process

Automated workflows are configured using GitHub Actions:

* Pull requests trigger build and test checks
* Only successful changes can be merged
* Merges to `main` trigger deployment to Azure

This process ensures reliability and consistency in releases.

---

## 🔐 Version Control Policy

* No direct commits to the `main` branch
* Pull requests are required for all changes
* Code must be reviewed before merging
* Automated checks must pass
* Force pushes and deletions are restricted

---

## 👥 Team

This project is developed collaboratively as part of the MSc Software Engineering programme.

---

## 📌 Purpose

The aim of this project is to apply industry-standard practices in a real-world scenario, demonstrating:

* Clean architecture design
* Effective team collaboration
* Automated testing and deployment
* Strong version control discipline

---

## 📄 Note

This project is developed for academic purposes as part of the MSc Software Engineering programme.
