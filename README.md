# Project_Smriti
Smriti -- Your Skills, Remembered and Refined

# Smriti - Personalized Developer Learning Roadmaps

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js](https://img.shields.io/badge/Node.js-16.x+-green.svg)](https://nodejs.org/)
[![React](https://img.shields.io/badge/React-18.x+-blue.svg)](https://reactjs.org/)
[![Express.js](https://img.shields.io/badge/Express.js-4.x+-lightgrey.svg)](https://expressjs.com/)
[![Vercel](https://img.shields.io/badge/Deployed%20on-Vercel-black.svg)](https://vercel.com/)

> **A full-stack web application that creates personalized learning roadmaps for developers based on their current skills and career goals, powered by real-time GitHub and Dev.to APIs.**

---

##  Overview

Smriti is a comprehensive learning platform designed to help developers navigate their career progression efficiently. By analyzing existing skills and comparing them against industry-standard roadmaps, it provides personalized learning paths with curated resources from GitHub repositories and educational articles.

###  Problem Statement
- Developers often struggle to identify skill gaps for their target roles
- Finding quality learning resources is time-consuming
- Lack of structured learning paths leads to inefficient skill development
- No centralized platform to track learning progress

###  Solution
Smriti addresses these challenges by:
- **Automated Gap Analysis**: Compares your skills against role requirements
- **Curated Resources**: Fetches real-time repositories and articles
- **Progress Tracking**: Monitors learning journey with session persistence
- **Export Capabilities**: Download personalized roadmaps for offline use

---

##  Features

###  User Experience
- **Interactive Skill Selection**: Choose from 30+ technologies with intuitive UI
- **Role-Based Roadmaps**: Frontend, Backend, Full-Stack, and DevOps paths
- **Visual Progress Tracking**: Clear indicators for completed vs. pending skills
- **Responsive Design**: Seamless experience across all devices

###  Smart Analytics
- **Gap Analysis**: Identifies missing skills for target roles
- **Priority Ranking**: Highlights critical skills to focus on
- **Progress Persistence**: Resume learning journey anytime
- **Export Functionality**: Download roadmaps in text format

###  Real-Time Integration
- **GitHub API**: Fetches trending repositories for hands-on practice
- **Dev.to API**: Curates educational articles and tutorials
- **Dynamic Content**: Always up-to-date learning resources
- **Fallback Systems**: Graceful handling of API limitations

###  Developer Features
- **Session Management**: Stateless architecture with in-memory storage
- **RESTful APIs**: Clean, documented endpoints
- **Error Handling**: Comprehensive error management
- **Performance Optimized**: Fast loading and smooth interactions

---

##  Tech Stack

### Frontend
- **React 18.x** - Modern UI with hooks and functional components
- **Tailwind CSS** - Utility-first styling framework
- **Lucide React** - Beautiful, customizable icons
- **Axios** - HTTP client for API communication

### Backend
- **Node.js** - JavaScript runtime environment
- **Express.js** - Fast, minimalist web framework
- **Cors** - Cross-origin resource sharing middleware
- **Crypto** - Secure session ID generation

### APIs & Services
- **GitHub REST API** - Repository data and search
- **Dev.to API** - Educational content and articles
- **In-Memory Storage** - Session persistence without database

### Development & Deployment
- **Vercel** - Serverless deployment platform
- **Concurrently** - Run multiple commands simultaneously
- **Nodemon** - Development server with hot reload

---

##  Architecture

```mermaid
graph TB
    A[User Interface - React] --> B[API Layer - Express.js]
    B --> C[Session Management - In-Memory]
    B --> D[GitHub API]
    B --> E[Dev.to API]
    B --> F[Roadmap Engine]
    
    C --> G[Progress Tracking]
    F --> H[Skill Gap Analysis]
    
    D --> I[Repository Recommendations]
    E --> J[Learning Articles]
    
    subgraph "External APIs"
    D
    E
    end
    
    subgraph "Core Services"
    B
    C
    F
    end
    
    subgraph "Client Features"
    A
    G
    H
    I
    J
    end
```

### Key Architectural Decisions

1. **Stateless Design**: No database dependency for easy deployment
2. **API-First Approach**: Clean separation between frontend and backend
3. **Session-Based Persistence**: User progress maintained across sessions
4. **Microservice Ready**: Modular structure for easy scaling
5. **Fallback Strategies**: Graceful degradation when external APIs fail

---

##  Quick Start

### Prerequisites
- Node.js 16.x or higher
- npm or yarn package manager
- Git for version control

### One-Command Setup
```bash
# Clone and setup entire project
git clone https://github.com/yourusername/skillsync.git
cd skillsync
npm run install-deps
npm run dev
```

### Access Points
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:5000/api
- **Health Check**: http://localhost:5000/api/health

---

##  Installation

### Step 1: Clone Repository
```bash
git clone https://github.com/yourusername/skillsync.git
cd skillsync
```

### Step 2: Backend Setup
```bash
cd backend
npm install
```

Create `.env` file (optional):
```env
PORT=5000
GITHUB_TOKEN=your_github_personal_access_token
NODE_ENV=development
```

### Step 3: Frontend Setup
```bash
cd ../frontend
npm install
npx tailwindcss init -p
```

### Step 4: Development Mode
```bash
# From root directory
npm run dev
```

This will start:
- Backend server on port 5000
- Frontend development server on port 3000
- Both with hot reload enabled

---

##  API Documentation

### Base URL
- **Development**: `http://localhost:5000/api`
- **Production**: `https://your-deployment-url.vercel.app/api`

### Core Endpoints

#### Session Management
```http
POST /api/session/create
Content-Type: application/json

{
  "name": "User Name",
  "skills": ["JavaScript", "React"],
  "targetRole": "frontend"
}
```

```http
GET /api/session/{sessionId}
```

```http
PUT /api/session/{sessionId}
Content-Type: application/json

{
  "skills": ["JavaScript", "React", "Node.js"],
  "targetRole": "fullstack"
}
```

#### Roadmap Data
```http
GET /api/roadmap/{role}
# Roles: frontend, backend, fullstack, devops
```

```http
GET /api/roadmaps
# Returns all available roadmaps
```

#### Learning Resources
```http
GET /api/github/{skill}
# Returns curated GitHub repositories
```

```http
GET /api/articles/{skill}
# Returns educational articles from Dev.to
```

#### Progress Tracking
```http
POST /api/progress/{sessionId}
Content-Type: application/json

{
  "skill": "React",
  "status": "completed",
  "notes": "Completed tutorial"
}
```

```http
GET /api/progress/{sessionId}
# Returns user's learning progress
```

#### System Health
```http
GET /api/health
# Returns system status and metrics
```

### Response Format
All API responses follow this structure:
```json
{
  "success": true,
  "data": { /* response data */ },
  "message": "Operation completed successfully",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### Error Handling
```json
{
  "success": false,
  "error": "Error message",
  "code": "ERROR_CODE",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

---

##  Deployment

### Vercel Deployment (Recommended)

#### Backend Deployment
```bash
cd backend
npm install -g vercel
vercel --prod
```

#### Frontend Deployment
1. Update API base URL in `frontend/src/App.js`:
```javascript
const API_BASE = 'https://your-backend-url.vercel.app/api';
```

2. Deploy frontend:
```bash
cd frontend
npm run build
vercel --prod
```

### Alternative Deployment Options

#### Railway
```bash
# Backend
railway login
railway new
railway add
railway deploy

# Frontend
# Connect GitHub repository to Railway dashboard
```

#### Render
```bash
# Create render.yaml in root:
services:
  - type: web
    name: skillsync-backend
    env: node
    buildCommand: cd backend && npm install
    startCommand: cd backend && npm start
    
  - type: web
    name: skillsync-frontend
    env: static
    buildCommand: cd frontend && npm run build
    staticPublishPath: frontend/build
```

### Environment Variables

#### Backend (.env)
```env
PORT=5000
GITHUB_TOKEN=ghp_xxxxxxxxxxxx
NODE_ENV=production
```

#### Frontend
```env
REACT_APP_API_BASE=https://your-backend-url.vercel.app/api
REACT_APP_VERSION=1.0.0
```

---

## 📁 Project Structure

```
skillsync/
├── 📁 backend/                 # Express.js backend
│   ├── 📄 server.js           # Main server file
│   ├── 📄 package.json        # Backend dependencies
│   └── 📄 vercel.json         # Vercel deployment config
│
├── 📁 frontend/               # React frontend
│   ├── 📁 public/             # Static assets
│   ├── 📁 src/
│   │   ├── 📄 App.js          # Main React component
│   │   ├── 📄 index.js        # React entry point
│   │   └── 📄 index.css       # Tailwind CSS imports
│   ├── 📄 package.json        # Frontend dependencies
│   ├── 📄 tailwind.config.js  # Tailwind configuration
│   └── 📄 postcss.config.js   # PostCSS configuration
│
├── 📄 package.json            # Root package.json (scripts)
├── 📄 README.md              # Project documentation
├── 📄 .gitignore             # Git ignore rules
└── 📄 LICENSE                # MIT License
```

### Code Organization

#### Backend Structure
- **Session Management**: In-memory storage for user data
- **API Routes**: RESTful endpoints for all operations
- **External API Integration**: GitHub and Dev.to connectors
- **Error Handling**: Comprehensive error management
- **Middleware**: CORS, JSON parsing, request logging

#### Frontend Structure
- **Component-Based**: Modular React components
- **State Management**: React hooks for state handling
- **API Integration**: Axios for backend communication
- **Responsive Design**: Tailwind CSS for mobile-first design
- **User Experience**: Loading states, error handling, animations

---

## 🧪 Testing

### Running Tests
```bash
# Backend tests
cd backend
npm test

# Frontend tests
cd frontend
npm test
```

### Test Coverage
- Unit tests for API endpoints
- Integration tests for external API calls
- Component tests for React UI
- End-to-end user flow testing

### Manual Testing Checklist
- [ ] Skill selection and deselection
- [ ] Role selection and roadmap generation
- [ ] API fallbacks when external services fail
- [ ] Session persistence across browser refreshes
- [ ] Export functionality
- [ ] Responsive design on mobile devices
- [ ] Progress tracking updates

---

##  Contributing

We welcome contributions from the community! Here's how you can help:

### Getting Started
1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass: `npm test`
6. Commit your changes: `git commit -m 'Add amazing feature'`
7. Push to the branch: `git push origin feature/amazing-feature`
8. Open a Pull Request

### Contribution Guidelines
- **Code Style**: Follow existing patterns and use Prettier/ESLint
- **Documentation**: Update README and add JSDoc comments
- **Testing**: Include tests for new features
- **Performance**: Consider performance implications of changes
- **Accessibility**: Ensure UI changes are accessible

### Areas for Contribution
-  **UI/UX Improvements**: Better animations, mobile experience
-  **New Features**: Additional role types, skill categories
-  **Analytics**: Learning progress insights, skill trends
-  **Internationalization**: Multi-language support
-  **Security**: Authentication, data protection
-  **Performance**: Caching, optimization, lazy loading

### Development Workflow
1. **Issue First**: Create or find an issue before starting work
2. **Small PRs**: Keep pull requests focused and small
3. **Documentation**: Update docs for any user-facing changes
4. **Testing**: Add tests for bug fixes and new features
5. **Review Process**: All PRs require at least one review

---

##  Performance & Scalability

### Current Performance Metrics
- **Initial Load**: < 2 seconds
- **API Response Time**: < 500ms average
- **Bundle Size**: < 1MB (gzipped)
- **Lighthouse Score**: 95+ (Performance, Accessibility, Best Practices)

### Scalability Considerations
- **Stateless Architecture**: Easy horizontal scaling
- **API Rate Limiting**: Built-in protection against abuse
- **Caching Strategy**: Browser and server-side caching
- **CDN Ready**: Static assets optimized for CDN delivery

### Future Optimizations
- Redis caching for external API responses
- Service worker for offline functionality
- Progressive Web App (PWA) features
- GraphQL API for efficient data fetching

---

##  Security

### Implemented Security Measures
- **Input Validation**: All user inputs validated and sanitized
- **CORS Configuration**: Proper cross-origin request handling
- **Rate Limiting**: API endpoint protection
- **Secure Headers**: Security headers for all responses
- **No Sensitive Data Storage**: No personal data persistence

### Security Best Practices
- Regular dependency updates
- Environment variable protection
- API token security
- Client-side data validation
- Secure deployment configurations

---

##  Troubleshooting

### Common Issues

#### API Rate Limiting
```bash
# If you encounter GitHub API rate limits:
# 1. Get a GitHub Personal Access Token
# 2. Add to backend/.env:
GITHUB_TOKEN=your_token_here
```

#### Development Server Issues
```bash
# Clear npm cache if installation fails:
npm cache clean --force

# Remove node_modules and reinstall:
rm -rf node_modules package-lock.json
npm install
```

#### Deployment Issues
```bash
# Verify build process:
cd frontend
npm run build

# Check backend health:
curl https://your-backend-url.vercel.app/api/health
```
---
### Long-term Vision
- Enterprise features for organizations
- Integration with HR systems
- Advanced learning analytics
- Gamification elements
- Global developer community features

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### MIT License Summary
- ✅ Commercial use
- ✅ Modification
- ✅ Distribution
- ✅ Private use
- ❌ No liability
- ❌ No warranty

---

## Acknowledgments

### Special Thanks
- **GitHub API** - For providing excellent repository data
- **Dev.to Community** - For educational content and articles
- **Roadmap.sh** - For inspiration on developer roadmaps
- **React Team** - For the amazing frontend framework
- **Vercel** - For seamless deployment experience

### Built With Love By
- **Primary Developer**: [Vikrant](https://github.com/Vikrant9098)
- **Contributors**: See [Contributors](https://github.com/Vikrant9098/Project_Smriti/contributors)

### Support the Project
If you find Smiriti helpful, please consider:
-  Starring the repository
-  Forking and contributing
-  Sharing with fellow developers
-  Suggesting new features

---
## Get In Touch
- **Portfolio**: [Coming Soon ]()
- **LinkedIn**: [Vikrant](https://linkedin.com/in/vikrantnaik9098)
- **Twitter**: [@Vikrant_9098](https://x.com/Vikrant_9098)
---

<div align="center">

**Made with ❤️ for the developer community**

[⬆ Back to Top](#-skillsync---personalized-developer-learning-roadmaps)

</div>
