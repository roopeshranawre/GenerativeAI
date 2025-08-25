# TrustTeams

A platform for discovering, posting, and managing internship opportunities.

## Overview

TrustTeams connects students and early-career talent with companies offering internships. Employers can post roles and manage applicants. Candidates can discover roles, filter by interests, and apply with a profile or resume.

## Users & Roles

- Candidate: Creates profile, searches roles, applies, tracks application status.
- Employer: Posts internships, manages applications, communicates with candidates.
- Admin: Moderates content, manages users/companies, handles reports/abuse.

## MVP Feature Set

- Authentication: Candidate and Employer sign up/sign in (email/password; OAuth optional later)
- Employer Job Posting: Create, edit, publish/unpublish internship listings
- Discovery: List internships with search, filters (location, type, paid/unpaid, skills, posted date)
- Applications: Candidates apply to postings with profile + resume; Employers view pipeline
- Candidate Profile: Basic info, education, skills, resume upload/link
- Notifications: Email confirmations for application submission and employer updates
- Admin Tools: Basic moderation of postings and user accounts

## Nice-to-Have (Post-MVP)

- Company pages and verification status
- Saved searches and job alerts
- In-app messaging between candidates and employers
- Candidate recommendations to employers
- Interview scheduling and feedback tracking
- Analytics dashboards for employers

## Core Data Model (first pass)

- User (id, name, email, role: candidate|employer|admin, createdAt)
- CandidateProfile (userId, education, skills[], links[], resumeUrl)
- Company (id, name, website, description, verified)
- Internship (id, companyId, title, description, location, employmentType, isPaid, minPay, maxPay, skills[], createdAt, status: draft|published|closed)
- Application (id, internshipId, candidateId, status: submitted|reviewing|interviewing|offer|rejected, coverLetter, attachments[], submittedAt, updatedAt)
- Audit/Moderation events as append-only logs

## API Sketch (REST)

- Auth
  - POST /api/auth/register
  - POST /api/auth/login
- Internships
  - GET /api/internships?query&filters
  - POST /api/internships (employer)
  - GET /api/internships/:id
  - PATCH /api/internships/:id (employer)
- Applications
  - POST /api/internships/:id/applications (candidate)
  - GET /api/employer/applications?status (employer)
  - PATCH /api/applications/:id (employer updates status)
- Profiles
  - GET/PUT /api/profile (candidate)
- Admin
  - GET/PATCH /api/admin/internships/:id
  - GET/PATCH /api/admin/users/:id

## Non-Functional Requirements

- Security: Role-based access control; per-resource ownership checks
- Privacy: Protect PII and resumes; encrypt at rest where appropriate
- Reliability: Idempotent endpoints for updates; pagination for list endpoints
- Observability: Request logging, error tracking, minimal metrics initially

## Suggested Tech Stack (flexible)

- Backend: Node.js (NestJS/Express) or Python (FastAPI)
- Frontend: Next.js/React with TypeScript
- Database: PostgreSQL (Prisma/SQLAlchemy)
- Auth: JWT + refresh tokens; provider-based OAuth later
- Storage: S3-compatible for resumes
- Infrastructure: Docker; deploy to a managed platform (Railway/Render/Fly/Heroku)

## Milestones

1. Week 1: Auth, basic models, seed data, list/detail internships
2. Week 2: Employer posting, candidate profile, applications
3. Week 3: Search/filters, employer application views, emails
4. Week 4: Admin moderation, polish, beta launch

## Getting Started (to be updated when code is added)

1. Install dependencies
2. Configure environment variables
3. Run database migrations
4. Start backend and frontend

# GenerativeAI