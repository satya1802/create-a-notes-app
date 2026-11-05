# Deployment Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start how-it-deploys -->
Pushes to `main` run `.github/workflows/deploy.yml`, which builds the API image (if there is a backend) and deploys the SPA to AWS Amplify. Commits touching only `docs/sdlc/**` don't deploy. Deployments can also be started from the platform's Deployment tab.
<!-- sdlc:auto:end how-it-deploys -->

<!-- sdlc:auto:start environments -->
| Name | Service | Runtime | Scaling | Environment |
|---|---|---|---|---|
| PWA Static Hosting | AWS S3 + CloudFront | Static React 19 build with service worker | CDN edge cache | dev |
| Notes API | AWS App Runner | FastAPI 0.115 on Python 3.12 (Uvicorn) | 1 instance, auto-scale on request load | dev |
| Database | AWS RDS for PostgreSQL 16 | PostgreSQL 16 | Single instance, automated backups, encryption at rest | dev |
| Email | SendGrid | SaaS API | Managed by provider | dev |
<!-- sdlc:auto:end environments -->

<!-- sdlc:auto:start live -->
_Not deployed yet._
<!-- sdlc:auto:end live -->

<!-- sdlc:auto:start topology -->
```mermaid
graph LR
  n_PWA_Static_Hosting["PWA Static Hosting<br/>AWS S3 + CloudFront"]
  n_Notes_API["Notes API<br/>AWS App Runner"]
  n_Database["Database<br/>AWS RDS for PostgreSQL 16"]
  n_Email["Email<br/>SendGrid"]
  n_PWA_Static_Hosting -->|"HTTPS"| n_Notes_API
  n_Notes_API -->|"TLS/PostgreSQL"| n_Database
  n_Notes_API -->|"HTTPS"| n_Email
```
<!-- sdlc:auto:end topology -->
