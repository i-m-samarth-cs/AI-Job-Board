# KPI Tech AI Job Board

A dynamic full-stack job board application with AI-powered candidate-to-job matching capabilities.

## Project Overview

This application serves two primary user roles:
1. **Company Admin** - Create and manage job listings, track applications
2. **Candidate** - Browse jobs, create profiles, and use AI-powered job matching

## Key Features

### Admin Features
- Create and edit job listings
- Manage job status (Open/Closed)
- View all applications per job
- Update application status (Applied → Shortlisted → Rejected)
- Dashboard with analytics and charts

### Candidate Features
- Create comprehensive candidate profiles
- Browse and search jobs with filters
- Apply to jobs
- AI-powered job matching with natural language queries
- Personal dashboard

### AI Matching
- Natural language job preference input
- Hybrid matching system (rule-based + LLM enhancement)
- Fallback to deterministic scoring when LLM is unavailable
- Detailed match explanations

## Tech Stack

### Frontend
- React 18 with Vite
- React Router for navigation
- Tailwind CSS for styling
- Axios for API calls
- Recharts for dashboard analytics
- React Hook Form for forms

### Backend
- FastAPI with Python 3.8+
- SQLAlchemy ORM with SQLite
- Pydantic for data validation
- Uvicorn ASGI server
- httpx for OpenRouter API integration

## Project Structure

```
kpi-tech-job-board/
├── README.md
├── backend/
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py
│   │   ├── database.py
│   │   ├── models/
│   │   │   ├── __init__.py
│   │   │   ├── job.py
│   │   │   ├── candidate.py
│   │   │   └── application.py
│   │   ├── schemas/
│   │   │   ├── __init__.py
│   │   │   ├── job.py
│   │   │   ├── candidate.py
│   │   │   └── application.py
│   │   ├── routers/
│   │   │   ├── __init__.py
│   │   │   ├── jobs.py
│   │   │   ├── candidates.py
│   │   │   ├── applications.py
│   │   │   ├── dashboard.py
│   │   │   └── ai_match.py
│   │   ├── services/
│   │   │   ├── __init__.py
│   │   │   ├── matching_service.py
│   │   │   ├── llm_service.py
│   │   │   └── seed_service.py
│   │   └── utils/
│   │       ├── __init__.py
│   │       └── helpers.py
│   ├── requirements.txt
│   └── .env.example
├── frontend/
│   ├── package.json
│   ├── vite.config.js
│   ├── tailwind.config.js
│   ├── index.html
│   ├── .env.example
│   └── src/
│       ├── main.jsx
│       ├── App.jsx
│       ├── components/
│       │   ├── common/
│       │   ├── admin/
│       │   └── candidate/
│       ├── pages/
│       │   ├── Landing.jsx
│       │   ├── admin/
│       │   └── candidate/
│       ├── services/
│       │   └── api.js
│       ├── hooks/
│       ├── types/
│       ├── layouts/
│       └── utils/
└── .gitignore
```

## System Architecture

### Backend Architecture
- **FastAPI** provides async API endpoints with automatic OpenAPI documentation
- **SQLAlchemy** handles database operations with SQLite for simplicity
- **Modular structure** separates concerns into routers, services, models, and schemas
- **Hybrid matching** combines deterministic scoring with optional LLM enhancement

### Frontend Architecture
- **React with Vite** for fast development and building
- **Component-based** architecture with reusable UI components
- **Service layer** abstracts API calls
- **Role-based routing** with mock authentication for demo purposes

### AI Matching System
1. **Natural Language Input** - Candidate describes preferences in plain English
2. **LLM Processing** - OpenRouter API extracts structured preferences (optional)
3. **Rule-based Ranking** - Weighted scoring system:
   - Skill overlap: 40%
   - Role relevance: 20%
   - Location match: 15%
   - Experience match: 10%
   - Domain match: 15%
4. **Explanation Generation** - LLM or template-based explanations

## Design Decisions

### Why FastAPI?
- Automatic API documentation with Swagger
- Excellent async support for AI API calls
- Strong typing with Pydantic
- Fast development and excellent Python ecosystem

### Why React?
- Component reusability
- Large ecosystem and community
- Excellent developer experience with Vite
- Easy to demonstrate and explain

### Why Hybrid Ranking?
- **Reliability** - App works without LLM dependency
- **Performance** - Fast deterministic scoring
- **Enhancement** - LLM adds natural language understanding
- **Cost Control** - Reduces API calls

### Why SQLite?
- Zero configuration database
- Perfect for demo and development
- Easy to inspect and debug
- Sufficient for interview requirements

### Why Mock Authentication?
- Focuses on core features rather than auth complexity
- Faster development within 3-day constraint
- Easy to demonstrate different user roles
- Production auth can be added later

## Environment Variables

### Backend (.env)
```
GROQ_API_KEY=your_groq_api_key_here
GROQ_MODEL=llama3-8b-8192
DATABASE_URL=sqlite:///./job_board.db
```

### Frontend (.env)
```
VITE_API_URL=http://localhost:8000
```

## Setup Instructions

### Prerequisites
- Python 3.8+ and pip
- Node.js 16+ and npm

### Quick Start

1. **Clone the repository**
   ```bash
   git clone <repo-url>
   cd kpi-tech-job-board
   ```

2. **Backend Setup**
   ```bash
   cd backend
   pip install -r requirements.txt
   cp .env.example .env
   # Edit .env file to add your OpenRouter API key (optional)
   python run.py
   ```
   Backend will start at http://localhost:8000

3. **Frontend Setup** (In a new terminal)
   ```bash
   cd frontend
   npm install
   cp .env.example .env
   npm run dev
   ```
   Frontend will start at http://localhost:5173

4. **Seed Demo Data**
   ```bash
   curl -X POST http://localhost:8000/seed-demo-data
   ```

5. **Access the Application**
   - Open http://localhost:5173 in your browser
   - Choose "Continue as Admin" or "Continue as Candidate"

### Alternative Backend Run Methods
```bash
# Using uvicorn directly
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload

# Using Python module
python -m app.main
```

## Demo Flow

### Admin Demo
1. Go to landing page → "Continue as Admin"
2. View dashboard with job and application analytics
3. Create a new job listing
4. View applications and update their status

### Candidate Demo  
1. Go to landing page → "Continue as Candidate"
2. Create/edit candidate profile
3. Browse jobs with filters
4. Use AI matching: "I want a Python backend role in a startup that does healthcare and allows remote work"
5. Apply to matched jobs

## 3-Day Build Plan

### Day 1: Foundation
- [ ] Project setup and folder structure
- [ ] Backend models and database setup
- [ ] Basic FastAPI endpoints (CRUD operations)
- [ ] Frontend React app with routing
- [ ] Basic UI components and layouts

### Day 2: Core Features
- [ ] Admin dashboard with job management
- [ ] Candidate profile and job browsing
- [ ] Application system
- [ ] Basic matching algorithm (deterministic)
- [ ] Charts and analytics

### Day 3: AI Enhancement & Polish
- [ ] OpenRouter LLM integration
- [ ] AI matching page with natural language input
- [ ] Seed data and testing
- [ ] UI polish and error handling
- [ ] Documentation and demo preparation

## What I Would Improve With More Time

### Technical Improvements
- **Authentication** - Implement proper JWT-based auth with role management
- **Database** - Migrate to PostgreSQL with proper indexing
- **Caching** - Add Redis for job search and matching results
- **API** - Implement pagination, rate limiting, and better error handling
- **Testing** - Add comprehensive unit and integration tests
- **Deployment** - Docker containers and CI/CD pipeline

### Feature Enhancements
- **Resume Processing** - PDF parsing and auto-profile population
- **Advanced Matching** - Vector embeddings for semantic job matching
- **Notifications** - Email/SMS alerts for application status changes
- **Analytics** - More detailed reporting and insights
- **File Uploads** - Resume storage and company logos
- **Real-time** - WebSocket updates for application status

### UI/UX Improvements
- **Design System** - Consistent component library
- **Accessibility** - WCAG compliance and screen reader support
- **Mobile** - Responsive design for mobile devices
- **Performance** - Code splitting and lazy loading
- **Offline** - Service worker for offline functionality

## Demo Script (30 minutes)

### Opening (5 minutes)
1. **Architecture Overview** - Show project structure and explain tech stack
2. **Problem Statement** - Explain the AI-powered job matching concept

### Admin Flow (10 minutes)
1. **Dashboard** - Show analytics and job overview
2. **Job Management** - Create new job, edit existing job
3. **Applications** - View applicants and update status
4. **Charts** - Demonstrate data visualization

### Candidate Flow (10 minutes)
1. **Profile Setup** - Create comprehensive candidate profile
2. **Job Browsing** - Show search and filter capabilities
3. **AI Matching** - Input natural language query and show results
4. **Application** - Apply to jobs and view application status

### Technical Deep Dive (5 minutes)
1. **Hybrid Matching** - Explain deterministic + LLM approach
2. **Fallback Strategy** - Show app working without LLM
3. **Code Structure** - Highlight clean, modular architecture
4. **Future Improvements** - Discuss scalability and enhancements

## Assumptions Made

1. **Authentication** - Mock authentication sufficient for demo
2. **Data Volume** - Small dataset appropriate for SQLite
3. **API Costs** - OpenRouter free tier sufficient for demo
4. **Browser Support** - Modern browsers only (Chrome, Firefox, Safari)
5. **Network** - Reliable internet connection for LLM calls
6. **Skills Format** - Comma-separated strings for simplicity
7. **File Uploads** - Text-based profiles only (no resume PDFs)
8. **Real-time** - Polling-based updates instead of WebSockets

## License

This project is created for interview demonstration purposes.

## Troubleshooting

### Common Issues

**Backend won't start:**
- Check Python version: `python --version` (should be 3.8+)
- Install dependencies: `pip install -r requirements.txt`
- Check port 8000 is not in use

**Frontend won't start:**
- Check Node version: `node --version` (should be 16+)
- Clear node_modules: `rm -rf node_modules && npm install`
- Check port 5173 is not in use

**Database errors:**
- Delete the database file: `rm job_board.db`
- Restart the backend to recreate tables

**AI matching not working:**
- The app works without OpenRouter API key (uses fallback)
- Add OPENROUTER_API_KEY to backend/.env for enhanced AI features

## API Documentation

Once the backend is running, visit:
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

## Demo Credentials

### Admin Access
- Role: Company Admin
- Features: Job management, application tracking, analytics

### Candidate Access  
- Role: Job Candidate
- Features: Profile management, job browsing, AI matching

*Note: This demo uses mock authentication. No actual login credentials required.*

## Architecture Details

### Backend Components
- **FastAPI**: REST API with automatic documentation
- **SQLAlchemy**: ORM with SQLite database
- **Pydantic**: Data validation and serialization
- **OpenRouter**: AI integration for natural language processing
- **Hybrid Matching**: Deterministic + AI-enhanced job scoring

### Frontend Components
- **React**: Component-based UI framework
- **Vite**: Fast development and build tooling
- **Tailwind CSS**: Utility-first styling
- **React Router**: Client-side routing
- **Recharts**: Data visualization
- **React Hook Form**: Form management

### Key Features Implementation

**AI-Powered Matching:**
1. Natural language query processing
2. Structured data extraction using LLM
3. Rule-based scoring algorithm
4. Fallback explanations when AI unavailable

**Admin Dashboard:**
1. Job posting and management
2. Application pipeline tracking
3. Interactive charts and analytics
4. Status management workflow

**Candidate Experience:**
1. Comprehensive profile creation
2. Advanced job search and filtering
3. One-click job applications
4. Application status tracking

## Production Deployment Considerations

### Security
- Implement proper JWT authentication
- Add input validation and rate limiting
- Use HTTPS with SSL certificates
- Add CORS configuration for specific domains

### Database
- Migrate from SQLite to PostgreSQL
- Implement database migrations
- Add proper indexing for performance
- Set up database backups

### Infrastructure
- Containerize with Docker
- Set up CI/CD pipeline
- Use environment-specific configurations
- Implement logging and monitoring

### Performance
- Add Redis caching for frequent queries
- Implement pagination for large datasets
- Optimize database queries
- Add CDN for static assets

## API Endpoints Summary

### Jobs
- `GET /jobs/` - List all jobs
- `POST /jobs/` - Create new job
- `GET /jobs/{id}` - Get job details
- `PUT /jobs/{id}` - Update job
- `PATCH /jobs/{id}/status` - Update job status
- `GET /jobs/search/` - Search jobs with filters

### Candidates
- `GET /candidates/{id}` - Get candidate profile
- `POST /candidates/` - Create candidate profile
- `PUT /candidates/{id}` - Update candidate profile

### Applications
- `POST /applications/` - Submit application
- `GET /applications/jobs/{job_id}` - Get job applications
- `PATCH /applications/{id}/status` - Update application status

### AI Matching
- `POST /ai/match` - AI-powered job matching

### Dashboard
- `GET /dashboard/admin-summary` - Admin analytics

### Utilities
- `GET /health` - Health check
- `POST /seed-demo-data` - Seed demo data

## Technology Decisions Deep Dive

### Why FastAPI over Flask/Django?
- **Automatic API documentation** with OpenAPI/Swagger
- **Type hints integration** with Pydantic for better code quality
- **Async support** for better performance with external API calls
- **Modern Python features** and excellent developer experience

### Why React over Vue/Angular?
- **Large ecosystem** with extensive component libraries
- **Excellent developer tools** and debugging capabilities
- **Strong typing** support with TypeScript (easily addable)
- **Wide industry adoption** making it interview-friendly

### Why SQLite over PostgreSQL?
- **Zero configuration** setup for development and demos
- **Portable** - single file database easy to share and backup
- **Sufficient performance** for demo-scale data
- **Easy migration** path to PostgreSQL for production

### Why Hybrid AI Matching?
- **Reliability** - Application works even when AI service is down
- **Cost control** - Reduces API calls to external services
- **Performance** - Fast deterministic scoring as baseline
- **Transparency** - Users understand how matching works

## Performance Benchmarks

### Expected Performance (Local Development)
- **API Response Time**: < 200ms for typical requests
- **AI Matching**: 2-5 seconds depending on LLM service
- **Frontend Load Time**: < 2 seconds on first load
- **Database Queries**: < 50ms for typical operations

### Scalability Considerations
- **Current capacity**: 100+ jobs, 1000+ candidates
- **Bottlenecks**: LLM API rate limits, single-threaded SQLite
- **Scaling solutions**: Database migration, caching, load balancing

## Contributing Guidelines

### Code Style
- **Python**: Follow PEP 8, use type hints
- **JavaScript**: Use ES6+, follow Airbnb style guide
- **Components**: Keep components small and focused
- **API**: Follow REST conventions

### Development Workflow
1. Create feature branch from main
2. Implement changes with tests
3. Update documentation if needed
4. Submit pull request with clear description

### Testing Strategy
- **Backend**: Unit tests with pytest
- **Frontend**: Component tests with React Testing Library
- **Integration**: End-to-end tests with Playwright
- **API**: Contract tests with Postman/Newman

## License and Usage

This project is created for interview demonstration purposes. Feel free to use as a reference for learning full-stack development patterns, AI integration, and modern web application architecture.

---

**Built with ❤️ for interview success**

*For questions or clarifications about implementation decisions, architecture choices, or potential improvements, please refer to the codebase comments or contact the development team.*#   A I - J o b - B o a r d  
 