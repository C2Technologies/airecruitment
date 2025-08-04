TalentMatch is an AI-powered recruitment platform that automates and enhances talent acquisition. It's a full-stack TypeScript application designed for HR professionals and recruiters, offering intelligent candidate matching, multi-format document processing, LinkedIn-style candidate generation, bidirectional job matching, and a centralized candidate library. The platform aims to revolutionize recruitment through advanced AI and modern web technologies.

TalentMatch AI Recruitment Portal - Local Setup Handover Document
Overview
This document provides comprehensive instructions for setting up and running the TalentMatch AI Recruitment Portal in a local development environment outside of Replit. The application is a full-stack TypeScript project with React frontend, Express backend, and PostgreSQL database.

Prerequisites
Required Software
Node.js: Version 18.0 or higher
npm: Version 8.0 or higher (comes with Node.js)
PostgreSQL: Version 13 or higher
Git: For version control
System Requirements
OS: Windows 10+, macOS 10.15+, or Linux (Ubuntu 20.04+)
RAM: Minimum 8GB, recommended 16GB
Storage: At least 2GB free space
Internet: Required for initial setup and AI features
Environment Setup
1. Clone the Repository
git clone <repository-url>
cd talentmatch-recruitment-portal
2. Install Dependencies
npm install
3. Database Setup
Option A: Local PostgreSQL Installation
Install PostgreSQL from https://postgresql.org/download/
Create a new database:
CREATE DATABASE talentmatch_dev;
CREATE USER talentmatch_user WITH PASSWORD 'your_secure_password';
GRANT ALL PRIVILEGES ON DATABASE talentmatch_dev TO talentmatch_user;
Option B: Docker PostgreSQL (Recommended)
# Create and run PostgreSQL container
docker run --name talentmatch-postgres \
  -e POSTGRES_DB=talentmatch_dev \
  -e POSTGRES_USER=talentmatch_user \
  -e POSTGRES_PASSWORD=your_secure_password \
  -p 5432:5432 \
  -d postgres:15
4. Environment Variables
Create a .env file in the root directory:

# Database Configuration
DATABASE_URL="postgresql://talentmatch_user:your_secure_password@localhost:5432/talentmatch_dev"
PGHOST=localhost
PGPORT=5432
PGUSER=talentmatch_user
PGPASSWORD=your_secure_password
PGDATABASE=talentmatch_dev
# Application Configuration
NODE_ENV=development
PORT=5000
SESSION_SECRET=your_very_secure_session_secret_key_here
# AI Integration (Required for full functionality)
OPENAI_API_KEY=your_openai_api_key_here
# Optional: Anthropic AI (if using alternative AI features)
ANTHROPIC_API_KEY=your_anthropic_api_key_here
5. Database Migration
# Push database schema
npm run db:push
# Alternative: Generate and run migrations
npm run db:generate
npm run db:migrate
Running the Application
Development Mode
# Start both frontend and backend in development mode
npm run dev
This command will:

Start the Express server on port 5000
Start the Vite development server
Enable hot module replacement (HMR)
Automatically restart on file changes
Production Build
# Build the application
npm run build
# Start production server
npm start
Individual Services
# Backend only
npm run server
# Frontend only (in separate terminal)
npm run client
Application Access
Once running, access the application at:

Development: http://localhost:5000
Frontend Dev Server: http://localhost:5173 (if running separately)
Default Login Credentials
Email: andrew@lortechnologies.com
Password: Pass.123
Project Structure
talentmatch-recruitment-portal/
├── client/                 # React frontend
│   ├── src/
│   │   ├── components/     # Reusable UI components
│   │   ├── pages/         # Application pages
│   │   ├── hooks/         # Custom React hooks
│   │   ├── lib/           # Utility functions
│   │   └── App.tsx        # Main application component
│   └── index.html         # HTML template
├── server/                # Express backend
│   ├── index.ts          # Server entry point
│   ├── routes.ts         # API routes
│   ├── storage.ts        # Database operations
│   ├── auth.ts           # Authentication logic
│   └── db.ts             # Database connection
├── shared/               # Shared types and schemas
│   └── schema.ts         # Database schema and types
├── uploads/              # File upload storage
├── package.json          # Dependencies and scripts
└── .env                  # Environment variables
Available Scripts
# Development
npm run dev              # Start full development environment
npm run server           # Start backend only
npm run client           # Start frontend only
# Database
npm run db:push          # Push schema changes to database
npm run db:generate      # Generate migration files
npm run db:migrate       # Run pending migrations
npm run db:studio        # Open Drizzle Studio (database GUI)
# Build & Production
npm run build           # Build for production
npm start              # Start production server
npm run preview        # Preview production build
# Utilities
npm run type-check     # TypeScript type checking
npm run lint           # Code linting
Configuration Details
Database Schema
The application uses Drizzle ORM with the following main tables:

users - User authentication and profiles
job_roles - Job postings and requirements
candidates - Candidate profiles and CVs
candidate_matches - AI-generated candidate-job matches
messages - Recruitment communications
sessions - User session storage
Authentication
Traditional email/password authentication
bcryptjs password hashing
PostgreSQL session storage
"Remember me" functionality
Secure session management
AI Integration
OpenAI GPT-4 for candidate analysis
Automatic match scoring (75-95% accuracy)
Skills assessment and red flag identification
Document processing and text extraction
Troubleshooting
Common Issues
Port Already in Use
# Find and kill process using port 5000
lsof -ti:5000 | xargs kill -9
# Or use different port
PORT=3000 npm run dev
Database Connection Issues
Verify PostgreSQL is running
Check database credentials in .env
Ensure database exists and user has permissions
Test connection: psql -h localhost -U talentmatch_user -d talentmatch_dev
Missing Environment Variables
Ensure .env file exists in root directory
Verify all required variables are set
Check for trailing spaces or quotes in values
OpenAI API Issues
Verify API key is valid and has credits
Check API rate limits
Ensure proper network connectivity
Development Tips
Hot Reloading
Frontend changes reload automatically
Backend restarts on TypeScript file changes
Database schema changes require npm run db:push
Debugging
Use browser dev tools for frontend debugging
Backend logs appear in terminal
Database queries can be monitored with Drizzle Studio
File Uploads
CV files are stored in uploads/ directory
Ensure directory has write permissions
Maximum file size: 10MB per file
Performance Optimization
Development
Use npm run dev with HMR for fastest development
Database indexes are optimized for common queries
Client-side caching with TanStack Query
Production
Build optimizations with Vite
Gzip compression enabled
Static asset caching
PostgreSQL connection pooling
Security Considerations
Local Development
Use strong passwords for database
Keep .env file secure and never commit to version control
Regularly update dependencies
Production Deployment
Use environment-specific configuration
Enable HTTPS
Configure proper CORS settings
Set up database backups
Monitor for security vulnerabilities
Support and Maintenance
Regular Maintenance
Update dependencies monthly: npm update
Monitor database performance and optimize queries
Review and rotate API keys quarterly
Backup database regularly
Logs and Monitoring
Application logs in console output
Database query logs available through Drizzle
Monitor API usage and rate limits
Track application performance metrics
Additional Resources
Drizzle ORM Documentation: https://orm.drizzle.team/
React Documentation: https://react.dev/
Express.js Guide: https://expressjs.com/
PostgreSQL Manual: https://www.postgresql.org/docs/
OpenAI API Reference: https://platform.openai.com/docs/
Contact Information
For technical questions or issues with the handover:

Review the comprehensive replit.md file for detailed project information
Check the troubleshooting section above
Refer to individual package documentation for specific issues
This handover document was created on August 4, 2025, for TalentMatch AI Recruitment Portal v1.0
