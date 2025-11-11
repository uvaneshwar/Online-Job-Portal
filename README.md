**Secure Job Portal **
1. Project Summary

A cloud-based job portal with separate roles for Employers and Job Seekers.

Uses Supabase PostgreSQL as the cloud database.

Frontend hosted on Heroku with auto-deployment from GitHub.

All authentication and data operations handled using SQL queries and cloud storage.

2. Key Cloud Components

Supabase

Provides managed PostgreSQL database.

Offers row-level security (RLS).

Provides cloud storage for resumes.

Real-time logs and monitoring.

API keys for secure backend communication.

Heroku

Hosts the frontend (HTML/CSS/JS).

Connected to GitHub for continuous deployment.

Environment variables stored as Heroku Config Vars.

HTTPS deployment with automatic build pipelines.

3. Database Structure (PostgreSQL)

users table

user_id (PK)

name, email, password_hash

role (job_seeker / employer)

created_at

jobs table

job_id (PK)

employer_id (FK)

title, description, salary, location

posted_at

applications table

application_id (PK)

job_id (FK)

seeker_id (FK)

resume_url (cloud storage link)

applied_at

SQL highlights

Normalized schema.

Primary/foreign key constraints.

Indexing on frequent search columns.

Secure access via SQL policies.

4. SQL Operations Used

Signup

Insert user record into users.

Hash password before insert.

Validate role input.

Login

SQL SELECT with password verification:

SELECT user_id, role 
FROM users 
WHERE email = $1 AND password_hash = crypt($2, password_hash);


Job Posting

INSERT INTO jobs (employer_id, title, description, salary, location)
VALUES ($1, $2, $3, $4, $5);


Job Applications

INSERT INTO applications (job_id, seeker_id, resume_url)
VALUES ($1, $2, $3);


Fetching Jobs / Applications

Uses JOIN queries for dashboards.

5. Cloud Workflow

Develop locally in VS Code.

Push changes to GitHub repository.

Heroku auto-deploys new commits.

Frontend communicates with Supabase using API keys.

SQL queries manage all platform operations.

6. Application Features

Role-based access

Employer dashboard: post jobs, view applications.

Job seeker dashboard: apply for jobs, upload resumes.

Cloud Resume Storage

Resumes uploaded to Supabase Storage bucket.

Stored URL referenced in SQL tables.

Secure Authentication

Credentials stored in PostgreSQL.

Validation through SQL-based logic.

Password hashing for security.
