# AI Personal Assistant - Full Stack Application

An intelligent personal productivity assistant built with React, Node.js, and Claude AI. This full-stack application helps you manage tasks, take smart notes, track productivity, and get AI-powered insights about your work patterns.

## 🌟 Features

### 📋 Task Management
- Create, read, update, and delete tasks
- Set priority levels (High, Medium, Low)
- Assign categories and due dates
- Track task status (Pending, In Progress, Completed)
- **AI-powered suggestions** for each task using Claude AI

### 📝 Smart Notes
- Create and organize notes with titles and tags
- Full-text search across notes
- **AI-generated summaries** of your notes
- Categorize with custom tags
- Edit and delete functionality

### 📊 Productivity Tracking
- Daily mood and focus level logging
- Hours worked tracking
- Daily notes and observations
- Real-time statistics (average mood, focus, total hours)
- Visual productivity history

### 🤖 AI Insights
- Generate personalized productivity insights
- Analyze task distribution and patterns
- Review productivity trends
- Get actionable recommendations to improve workflow
- Powered by Claude AI (Opus 4.1 model)

## 🏗️ Architecture

### Frontend
- **React 18** - UI library
- **Axios** - HTTP client
- **Lucide React** - Icon library
- **CSS3** - Modern styling with gradients and animations
- Responsive design for mobile and desktop

### Backend
- **Node.js + Express.js** - Web server and API
- **SQLite3** - Lightweight relational database
- **Anthropic SDK** - Claude AI integration
- **CORS** - Cross-origin resource sharing support

### Database Schema
```
Tables:
- tasks (id, title, description, priority, status, category, dueDate, aiSuggestion, timestamps)
- notes (id, title, content, aiSummary, tags, timestamps)
- productivity (id, date, mood, focusLevel, hoursWorked, notes, timestamps)
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn
- Anthropic API key (get one at https://console.anthropic.com)

### Installation

1. **Clone the repository**
```bash
git clone <repository-url>
cd ai-personal-tool
```

2. **Backend Setup**
```bash
cd backend

# Install dependencies
npm install

# Create .env file
cp .env.example .env

# Add your Anthropic API key to .env
# ANTHROPIC_API_KEY=your_api_key_here

# Start the backend server
npm start
# Server will run on http://localhost:5000
```

3. **Frontend Setup**
```bash
cd ../frontend

# Install dependencies
npm install

# Create .env file (if needed)
cp .env.example .env

# Start the development server
npm start
# App will open at http://localhost:3000
```

## 📖 API Documentation

### Tasks Endpoints
- `GET /api/tasks` - Get all tasks (supports ?status=pending, ?category=work)
- `POST /api/tasks` - Create a new task
- `PUT /api/tasks/:id` - Update a task
- `DELETE /api/tasks/:id` - Delete a task

### Notes Endpoints
- `GET /api/notes` - Get all notes
- `POST /api/notes` - Create a new note
- `PUT /api/notes/:id` - Update a note
- `DELETE /api/notes/:id` - Delete a note

### Productivity Endpoints
- `GET /api/productivity` - Get productivity logs (supports ?startDate=2024-01-01)
- `POST /api/productivity` - Log a productivity entry

### Insights Endpoint
- `POST /api/insights` - Generate AI insights based on tasks and productivity data

## 🎨 UI Components

### Main Sections
1. **Tasks Section** - Full task management with AI suggestions
2. **Notes Section** - Smart note-taking with AI summaries
3. **Productivity Section** - Daily tracking with visual statistics
4. **Insights Section** - AI-powered analysis and recommendations

### Design Features
- Modern gradient header (purple to violet)
- Responsive card-based layout
- Color-coded status and priority badges
- Smooth animations and transitions
- Mobile-friendly navigation
- Empty states with helpful prompts

## 🤖 AI Integration

The application uses **Claude Opus 4.1** model for:

1. **Task Suggestions** - Provides actionable advice for each task
2. **Note Summarization** - Creates concise summaries of your notes
3. **Productivity Insights** - Analyzes patterns and suggests improvements

### Example AI Outputs
- Task: "Learn React Hooks" → Suggestion: "Focus on understanding useState and useEffect first, then explore custom hooks..."
- Note: "Long meeting transcript..." → Summary: "Team discussed Q4 goals, decided to shift focus to mobile optimization..."
- Insights: "You completed 12 tasks this week with good focus levels. Consider breaking down complex tasks into smaller subtasks..."

## 🗂️ Project Structure

```
ai-personal-tool/
├── backend/
│   ├── server.js              # Main Express server
│   ├── package.json           # Dependencies
│   ├── .env.example          # Environment template
│   └── assistant.db          # SQLite database (generated on first run)
│
├── frontend/
│   ├── public/
│   │   └── index.html        # HTML entry point
│   ├── src/
│   │   ├── App.js            # Main App component
│   │   ├── App.css           # Main styles
│   │   ├── index.js          # React entry point
│   │   ├── index.css         # Base styles
│   │   └── components/
│   │       ├── TasksSection.js       # Task management
│   │       ├── NotesSection.js       # Note-taking
│   │       ├── ProductivitySection.js # Productivity tracking
│   │       └── InsightsSection.js    # AI insights
│   ├── package.json          # Dependencies
│   └── .env.example          # Environment template
│
└── README.md                  # This file
```

## 🔧 Configuration

### Environment Variables

**Backend (.env)**
```
PORT=5000
ANTHROPIC_API_KEY=sk-ant-...
```

**Frontend (.env)**
```
REACT_APP_API_URL=http://localhost:5000/api
```

For production, change `REACT_APP_API_URL` to your deployed backend URL.

## 🚢 Deployment

### Frontend (Vercel/Netlify)
1. Build the React app: `npm run build`
2. Deploy the `build/` folder
3. Set environment variables in hosting platform

### Backend (Heroku/Railway/Render)
1. Push code to git repository
2. Connect repository to hosting platform
3. Set `ANTHROPIC_API_KEY` in environment variables
4. Deploy

## 📝 Example Workflows

### Creating a Task with AI Suggestions
1. Navigate to Tasks tab
2. Click "New Task"
3. Enter task title: "Design database schema for new project"
4. AI automatically suggests: "Start by identifying entities and relationships, then normalize the schema..."
5. Set priority and due date
6. Task is created and saved

### Taking Smart Notes
1. Go to Notes tab
2. Click "New Note"
3. Write detailed notes about a meeting or learning
4. AI generates a 2-3 sentence summary
5. Add tags for easy filtering
6. View AI summary on the note card

### Getting Daily Insights
1. Log your daily productivity (mood, focus, hours)
2. Go to Insights tab
3. Click "Generate Insights"
4. AI analyzes all your data and provides personalized recommendations

## 🎓 Learning Outcomes

This project demonstrates:
- ✅ Full-stack development (frontend + backend)
- ✅ React hooks and state management
- ✅ Express.js REST API design
- ✅ SQLite database operations
- ✅ API integration and async operations
- ✅ Responsive UI design
- ✅ Error handling and loading states
- ✅ Environment configuration
- ✅ AI/LLM integration
- ✅ Production-ready code structure

## 🐛 Troubleshooting

### Backend won't start
- Check if port 5000 is available
- Ensure Node.js version is 14+
- Verify ANTHROPIC_API_KEY is set correctly

### Frontend can't connect to backend
- Make sure backend is running on port 5000
- Check REACT_APP_API_URL in .env
- Clear browser cache and restart frontend

### AI features not working
- Verify ANTHROPIC_API_KEY is valid
- Check API rate limits
- Ensure you have credits on Anthropic account

## 📄 License

MIT License - Feel free to use this for personal and educational purposes.

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest features
- Improve documentation
- Submit pull requests

## 📚 Resources

- [Anthropic Claude Documentation](https://docs.anthropic.com)
- [React Documentation](https://react.dev)
- [Express.js Guide](https://expressjs.com)
- [SQLite Documentation](https://www.sqlite.org/docs.html)

## 💡 Future Enhancements

- [ ] User authentication and multi-user support
- [ ] Data export (CSV, PDF)
- [ ] Advanced filtering and sorting
- [ ] Task templates
- [ ] Recurring tasks
- [ ] Dark mode
- [ ] Mobile app (React Native)
- [ ] Real-time collaboration
- [ ] Cloud synchronization
- [ ] Advanced analytics dashboard

## 🎯 Project Stats

- **Lines of Code:** ~2000+
- **Components:** 5
- **API Endpoints:** 12+
- **Database Tables:** 3
- **Responsive Breakpoints:** Mobile, Tablet, Desktop

---

**Built with ❤️ using React, Node.js, and Claude AI**

*Perfect for your CS portfolio and GitHub profile!*
