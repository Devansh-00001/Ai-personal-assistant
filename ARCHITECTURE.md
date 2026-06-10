# System Architecture

## Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                      USER BROWSER                               │
│                    (http://localhost:3000)                      │
└─────────────────────────────────────────────────────────────────┘
                              ↓
                    ┌──────────────────┐
                    │   REACT FRONTEND │
                    │   (Components)   │
                    └──────────────────┘
                              ↓
        ┌─────────────────────────────────────────┐
        │   AXIOS HTTP REQUESTS (JSON)            │
        │   http://localhost:5000/api/*           │
        └─────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│                    EXPRESS.JS SERVER                            │
│              (http://localhost:5000)                            │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │            ROUTE HANDLERS & LOGIC                       │   │
│  │  • POST /api/tasks        - Create task                 │   │
│  │  • GET  /api/tasks        - Fetch tasks                 │   │
│  │  • PUT  /api/tasks/:id    - Update task                 │   │
│  │  • DELETE /api/tasks/:id  - Delete task                 │   │
│  │  • POST /api/notes        - Create note                 │   │
│  │  • ... (and more)                                       │   │
│  └─────────────────────────────────────────────────────────┘   │
│                              ↓                                   │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │         CLAUDE AI INTEGRATION (Anthropic SDK)           │   │
│  │  • Task Suggestions                                     │   │
│  │  • Note Summarization                                   │   │
│  │  • Productivity Insights                                │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              ↓
        ┌─────────────────────────────────────────┐
        │      SQLITE3 DATABASE                   │
        │  (assistant.db - Local File)            │
        │                                         │
        │  Tables:                                │
        │  • tasks (task management)              │
        │  • notes (note storage)                 │
        │  • productivity (tracking data)         │
        └─────────────────────────────────────────┘
```

## Component Architecture

### Frontend Components

```
App.js (Main Container)
├── TasksSection
│   ├── Create Form
│   ├── Filter Controls
│   ├── AI Suggestions Display
│   └── Task Cards (with update/delete)
├── NotesSection
│   ├── Create/Edit Form
│   ├── Search Filter
│   ├── AI Summary Display
│   └── Note Cards
├── ProductivitySection
│   ├── Log Form
│   ├── Statistics Dashboard
│   └── Entry History
└── InsightsSection
    ├── Generate Button
    └── AI Insights Display
```

### Backend Structure

```
server.js
├── Database Initialization
├── Express App Setup
├── CORS & Middleware
├── Task Endpoints
│   ├── GET /api/tasks
│   ├── POST /api/tasks
│   ├── PUT /api/tasks/:id
│   └── DELETE /api/tasks/:id
├── Notes Endpoints
│   ├── GET /api/notes
│   ├── POST /api/notes
│   ├── PUT /api/notes/:id
│   └── DELETE /api/notes/:id
├── Productivity Endpoints
│   ├── GET /api/productivity
│   └── POST /api/productivity
├── Insights Endpoint
│   └── POST /api/insights
├── AI Helper Functions
│   ├── generateTaskSuggestion()
│   ├── generateNoteSummary()
│   └── generateInsights()
└── Error Handling
```

## Data Flow Examples

### Task Creation Flow

```
1. User fills form → Click "Create Task"
   ↓
2. TasksSection.js validates input
   ↓
3. Axios POST to /api/tasks with task data
   ↓
4. server.js receives request
   ↓
5. Calls generateTaskSuggestion() with Claude API
   ↓
6. Inserts task + aiSuggestion into SQLite
   ↓
7. Returns response to frontend
   ↓
8. TasksSection refreshes via onTasksChange()
   ↓
9. New task appears in UI with AI suggestion ✨
```

### Note Summarization Flow

```
1. User enters note content
   ↓
2. Axios POST to /api/notes
   ↓
3. server.js calls generateNoteSummary()
   ↓
4. Sends note content to Claude API
   ↓
5. Claude generates 2-3 sentence summary
   ↓
6. Saves note + aiSummary to SQLite
   ↓
7. Returns response
   ↓
8. Frontend displays note with "AI Summary" badge
```

### Insights Generation Flow

```
1. User clicks "Generate Insights"
   ↓
2. Frontend POST to /api/insights
   ↓
3. backend fetches all pending tasks
   ↓
4. backend fetches recent productivity data
   ↓
5. Compiles summary of data
   ↓
6. Sends to Claude API for analysis
   ↓
7. Claude returns personalized insights
   ↓
8. Frontend displays insights in card
```

## Database Schema

### Tasks Table
```
tasks (
  id TEXT PRIMARY KEY,
  title TEXT NOT NULL,
  description TEXT,
  priority TEXT DEFAULT 'medium',      -- high, medium, low
  status TEXT DEFAULT 'pending',       -- pending, in-progress, completed
  category TEXT,                       -- Work, Personal, Learning, etc.
  dueDate TEXT,                        -- ISO date string
  aiSuggestion TEXT,                   -- Generated by Claude
  createdAt DATETIME,
  updatedAt DATETIME
)
```

### Notes Table
```
notes (
  id TEXT PRIMARY KEY,
  title TEXT NOT NULL,
  content TEXT NOT NULL,
  aiSummary TEXT,                      -- Generated by Claude
  tags TEXT,                           -- Comma-separated tags
  createdAt DATETIME,
  updatedAt DATETIME
)
```

### Productivity Table
```
productivity (
  id TEXT PRIMARY KEY,
  date TEXT NOT NULL,                  -- ISO date string
  mood TEXT,                           -- excellent, good, neutral, bad, terrible
  focusLevel INTEGER,                  -- 1-10 scale
  hoursWorked REAL,                    -- Decimal hours
  notes TEXT,                          -- User notes
  createdAt DATETIME
)
```

## API Response Examples

### Create Task Response
```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "title": "Learn React Hooks",
  "description": "Understand useState, useEffect, and custom hooks",
  "priority": "high",
  "category": "Learning",
  "dueDate": "2024-02-15",
  "aiSuggestion": "Start with useState basics, then explore useEffect lifecycle. Consider building a small project like a todo list to solidify understanding.",
  "status": "pending"
}
```

### Get Notes Response
```json
[
  {
    "id": "123...",
    "title": "AI Meeting Notes",
    "content": "Discussed Claude API...",
    "aiSummary": "Team reviewed Claude API capabilities and use cases for the project.",
    "tags": "meeting,ai,api",
    "createdAt": "2024-01-20T10:30:00"
  }
]
```

### Insights Response
```json
{
  "insights": "You have 5 high-priority tasks due this week. Your focus levels have been strong (avg 7.5/10) but mood is declining slightly. Consider breaking down complex tasks and taking more breaks. You're most productive in mornings based on your logs."
}
```

## Environment Variables

### Backend (.env)
```
PORT=5000
ANTHROPIC_API_KEY=sk-ant-xxxxxxxx...
```

### Frontend (.env)
```
REACT_APP_API_URL=http://localhost:5000/api
```

## Performance Considerations

### Frontend Optimizations
- Use React.memo for card components
- Implement debouncing for search
- Lazy load components if needed
- Cache API responses with timestamps

### Backend Optimizations
- Index frequently queried columns in SQLite
- Implement response caching for insights
- Rate limit API calls to Claude
- Use connection pooling for database

### Database Optimizations
```sql
-- Create indexes for faster queries
CREATE INDEX idx_tasks_status ON tasks(status);
CREATE INDEX idx_notes_tags ON notes(tags);
CREATE INDEX idx_productivity_date ON productivity(date);
```

## Deployment Architecture

```
Production Environment:
├── Frontend (Vercel/Netlify)
│   └── React build served as static site
├── Backend (Railway/Heroku/Render)
│   └── Node.js + SQLite
└── Domain & SSL (CloudFlare or similar)
    └── Reverse proxy to both services
```

## Security Considerations

1. **API Keys:**
   - Never commit .env files
   - Use environment variables
   - Rotate keys regularly

2. **CORS:**
   - Restrict to your domain in production
   - Use proxy for API calls

3. **Database:**
   - Use parameterized queries (already done with SQLite3 bindings)
   - Validate all inputs

4. **Rate Limiting:**
   - Add rate limiting for API endpoints
   - Implement request throttling for Claude API

## Monitoring & Logging

```javascript
// Add logging
console.log(`[${new Date().toISOString()}] ${method} ${path}`);

// Error tracking
try {
  // operation
} catch (error) {
  console.error('Error:', error.message);
  // Send to error tracking service
}
```

---

This architecture is production-ready and demonstrates solid full-stack development practices!
