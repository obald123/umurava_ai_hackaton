# Umurava AI Talent Screening - Zuba Tech Team

**Hackathon Challenge: An Innovation Challenge to build AI Products for Human Resources Industry**

Production-ready prototype for an AI-powered recruiter screening workflow that augments recruiters' decision-making while keeping humans in control of final hiring decisions.

##  Problem Statement

Recruiters today face two major challenges:
- High application volumes that significantly increase time-to-hire
- Difficulty objectively comparing candidates across diverse profiles and formats

**Our Solution**: AI-powered talent profile screening tool that:
- Understands job requirements and ideal candidate profiles
- Analyzes multiple applicants at once using Gemini API
- Produces ranked shortlists (Top 10 or Top 20) with transparent reasoning
- Clearly explains why candidates were shortlisted

##  System Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │    Backend      │    │   Database      │
│   Next.js        │◄──►│   Node.js       │◄──►│   MongoDB       │
│   TypeScript     │    │   TypeScript     │    │   Atlas         │
│   Redux Toolkit  │    │   Express       │    │                 │
│   Tailwind CSS   │    │   JWT Auth      │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                │
                                ▼
                       ┌─────────────────┐
                       │   AI Layer      │
                       │   Gemini API    │
                       │   Prompt Eng.   │
                       └─────────────────┘
```

##  Technology Stack

**Mandatory Requirements Met:**
- **Language**: TypeScript 
- **Frontend**: Next.js 
- **State Management**: Redux + Redux Toolkit 
- **Styling**: Tailwind CSS 
- **Backend**: Node.js 
- **Database**: MongoDB 
- **AI/LLM**: Gemini API 

##  Quick Start

### 1) Backend Setup

```bash
cd backend
cp .env.example .env
npm install
npm run dev
```

**Environment Variables (.env):**
```bash
# Database
MONGODB_URI=mongodb+srv://...

# AI Configuration
GEMINI_API_KEY=your_gemini_api_key

# JWT Authentication
JWT_SECRET=your_jwt_secret
JWT_REFRESH_SECRET=your_jwt_refresh_secret
JWT_EXPIRE=15m
JWT_REFRESH_EXPIRE=7d

# Admin Credentials (use this on live site)
AUTH_EMAIL=admin@umurava.com
AUTH_PASSWORD=Admin123@...

# CORS Configuration
CORS_ORIGINS=http://localhost:3000
```

### 2) Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

**Environment Variables (.env.local):**
```bash
NEXT_PUBLIC_API_URL=http://localhost:4000
```

##  AI Decision Flow

### 1. Job & Candidate Compilation
```typescript
interface JobRequirements {
  title: string;
  requiredSkills: string[];
  experienceLevel: string;
  educationLevel: string;
  weights: { skills: 40, experience: 30, education: 15, relevance: 15 };
}
```

### 2. Gemini Multi-Candidate Evaluation
- **Single Prompt**: All candidates evaluated together for consistency
- **Weighted Scoring**: Skills (40%), Experience (30%), Education (15%), Relevance (15%)
- **Bias Awareness**: Structured prompts to reduce subjective bias

### 3. Structured AI Output
```typescript
interface AIResponse {
  candidates: [{
    rank: number;
    score: number; 
    strengths: string[];
    gaps: string[];
    recommendation: "Strong" | "Moderate" | "Weak";
    whyNotSelected?: string;
  }];
}
```

### 4. Explainable Results
- **Strengths**: Clear reasons for recommendation
- **Gaps**: Identified skill/experience gaps
- **Relevance**: How candidate matches job requirements
- **Confidence**: AI's confidence in evaluation

## API Endpoints

### Jobs Management
- `POST /jobs` - Create new job
- `GET /jobs` - List all jobs
- `GET /jobs/:id` - Get job details
- `PUT /jobs/:id` - Update job

### Applicants & Screening
- `POST /applicants` - Upload applicants (CSV/PDF/Manual)
- `POST /screen` - Trigger AI screening
- `GET /results/:jobId` - Get ranked candidates
- `POST /applicants/parse-pdf` - Parse PDF resumes
- `POST /applicants/parse-pdf-url` - Parse PDF from URL

### Authentication
- `POST /auth/login` - JWT login
- `POST /auth/refresh` - Refresh JWT token
- `POST /auth/logout` - Logout

## Frontend Features

### Recruiter Dashboard
- **Job Management**: Create, edit, view jobs
- **Applicant Upload**: CSV, PDF, manual entry
- **Screening Interface**: Trigger AI screening with progress tracking
- **Results Visualization**: Ranked shortlists with detailed reasoning
- **Candidate Cards**: Individual candidate analysis and actions

### User Experience
- **Responsive Design**: Works on desktop and mobile
- **Real-time Updates**: Live screening progress
- **Error Handling**: User-friendly error messages
- **Loading States**: Visual feedback during operations

## Security Implementation

### JWT Authentication
- **Access Tokens**: 15-minute expiry
- **Refresh Tokens**: 7-day expiry
- **Secure Storage**: HttpOnly cookies + localStorage
- **Automatic Refresh**: Seamless token renewal

### Data Protection
- **CORS Configuration**: Environment-based origin restrictions
- **Input Validation**: Sanitized data processing
- **Error Handling**: No sensitive data exposure



### Build Commands
```bash
# Frontend
npm install
npm run build
npm run start

# Backend
npm install
npm run build
npm run start
```


**Live Demo:** https://umurava-fe-gray.vercel.app 

