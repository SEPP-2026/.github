# SEPP-2026 - Shelton Tool-Hire Review Portal

SEPP-2026 hosts the Shelton Tool-Hire Review Portal, an MSc Software Engineering project for a full-stack tool-hire review and catalogue platform. The system is split into independent frontend, backend API, and QA automation repositories so each part can be tested, reviewed, and deployed with clear ownership.

## Project Repositories

| Repository | Purpose | Main technology |
|------------|---------|-----------------|
| [ReviewPortal-Web](https://github.com/SEPP-2026/ReviewPortal-Web) | Customer and staff web client for catalogue browsing, rental calculation, reviews, moderation, and admin workflows | Next.js, TypeScript, React |
| [ReviewPortal-API](https://github.com/SEPP-2026/ReviewPortal-API) | ASP.NET Core backend API, business logic, persistence, authentication, image storage, telemetry, and deployment workflow | .NET 8, ASP.NET Core, EF Core, SQL Server |
| [ReviewPortal-QA-Automation](https://github.com/SEPP-2026/ReviewPortal-QA-Automation) | Playwright smoke and regression tests against the deployed Review Portal environment | Playwright, TypeScript |
| [.github](https://github.com/SEPP-2026/.github) | Organization profile README and shared GitHub metadata | Markdown |

## Current System Capabilities

- Public tool catalogue browsing with categories, search, details, images, and rental cost calculation
- Customer registration, login, current-user lookup, password change, forgot-password, and reset-password flows
- JWT-based API authentication with role-based Customer, Moderator, and Admin access
- Customer review submission, review history, review comments, and company responses
- Moderator/Admin review and comment moderation
- Admin category, tool, status, and image management
- Admin dashboard statistics
- Azure Blob Storage for uploaded tool/service images
- Azure Application Insights support for API request telemetry, dependency telemetry, exceptions, and logs
- Swagger/OpenAPI documentation for the backend API
- Playwright QA automation for deployed frontend/API smoke coverage

## Architecture

The system uses a separated full-stack architecture:

```text
ReviewPortal-Web
        |
        v
ReviewPortal-API
        |
        v
Azure SQL Database

ReviewPortal-API -> Azure Blob Storage
ReviewPortal-API -> Azure Application Insights
GitHub Actions   -> Azure App Service
GitHub Actions   -> ReviewPortal-QA-Automation
```

The API follows Clean Architecture:

```text
Domain <- Application <- Infrastructure
                     <- API
```

This keeps business rules, persistence, HTTP concerns, and external Azure integrations separated.

## Technology Stack

| Area | Stack |
|------|-------|
| Frontend | Next.js, React, TypeScript, CSS modules/application styling |
| Backend | .NET 8, ASP.NET Core Web API, EF Core, SQL Server/Azure SQL |
| Authentication | JWT bearer tokens, ASP.NET Core password hashing, role-based authorization |
| Storage | Azure Blob Storage for durable image uploads |
| Monitoring | Azure Application Insights |
| API documentation | Swagger/OpenAPI |
| Automated tests | xUnit, FluentAssertions, Playwright |
| CI/CD | GitHub Actions, Azure App Service, GitHub protected environments |

## Branch And Release Workflow

The project uses a controlled branch workflow:

- Feature work is developed on feature branches.
- Pull requests target `development` first.
- Unit and integration tests must pass before merge.
- The `development` branch is used for integration and validation work, but it does not deploy the API to Azure.
- Production release changes are promoted from `development` to `main` through a reviewed pull request.
- API deployment to Azure App Service happens only from `main` after checks pass and the GitHub `production` environment is approved.
- Playwright QA automation is triggered after the successful `main` API workflow, or manually from `main`.

## CI/CD Overview

### ReviewPortal-API

- Pull requests to `development` and `main` run unit tests and integration tests.
- Pushes to `development` run unit tests and integration tests only.
- Pushes to `main` run unit tests and integration tests, publish the API, and deploy to Azure App Service after production approval.
- Integration tests run on Windows because the suite uses SQL Server LocalDB.
- Dependabot checks NuGet and GitHub Actions dependencies weekly and opens PRs into `development`.

### ReviewPortal-Web

- The frontend repository owns the customer/admin user interface and frontend deployment flow.
- It integrates with the deployed API through environment-specific API base URLs.
- Playwright tests validate key user journeys against the deployed system.

### ReviewPortal-QA-Automation

- Playwright tests run against configured Azure frontend and API URLs.
- QA runs can be triggered by repository dispatch from the API workflow.
- Smoke coverage includes public home/catalogue access and core deployed-environment checks.

## Azure Services

| Service | Use |
|---------|-----|
| Azure App Service | Hosts the deployed API and frontend applications |
| Azure SQL Database | Production relational database for catalogue, users, reviews, moderation, and admin data |
| Azure Blob Storage | Stores uploaded tool/service images outside the App Service filesystem |
| Azure Application Insights | Collects API telemetry, failures, performance data, logs, and live diagnostics |

Secrets and runtime settings are kept in GitHub Actions secrets, GitHub environments, Azure App Service environment variables, .NET user secrets, or ignored local settings files. Real connection strings, publish profiles, JWT secrets, storage keys, and tokens must not be committed.

## Quality And Security Practices

- Pull request review before promotion to protected branches
- Automated unit and integration tests for backend changes
- Playwright smoke/regression checks for deployed workflows
- Secret scanning helper scripts before opening PRs
- Main-only API deployment with a production approval gate
- Azure Blob Storage preferred over App Service local filesystem uploads
- Application Insights enabled through environment configuration rather than checked-in secrets
- Dependabot dependency update PRs targeting `development`

## Academic Purpose

This organization and its repositories support an MSc Software Engineering project. The implementation demonstrates practical use of modular architecture, automated testing, CI/CD, Azure cloud deployment, monitoring, secure configuration, and collaborative GitHub workflows.
