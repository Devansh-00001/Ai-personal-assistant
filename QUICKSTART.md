# 🚀 Quick Start Guide

## Prerequisites
- Node.js v14+ installed
- npm or yarn installed
- Anthropic API key (free from https://console.anthropic.com)

## Option 1: Local Development (Recommended for CS Projects)

### Step 1: Get Your API Key
1. Go to https://console.anthropic.com
2. Sign up or log in
3. Create an API key in the dashboard
4. Copy the key (looks like: `sk-ant-...`)

### Step 2: Backend Setup
```bash
cd backend

# Install dependencies
npm install

# Create .env file
echo "PORT=5000" > .env
echo "ANTHROPIC_API_KEY=your_api_key_here" >> .env

# Replace 'your_api_key_here' with your actual key

# Start the server
npm start
```

You should see:
```
Connected to SQLite database
Server running on http://localhost:5000
```

### Step 3: Frontend Setup (in a new terminal)
```bash
cd frontend

# Install dependencies
npm install

# Start the app
npm start
```

The app will open in your browser at `http://localhost:3000` 🎉

## Option 2: Docker (For Production/Deployment)

### Prerequisites
- Docker installed
- Anthropic API key

### Steps
```bash
# Create .env file in project root
echo "ANTHROPIC_API_KEY=your_api_key_here" > .env

# Run with docker-compose
docker-compose up --build

# Access the app at http://localhost:3000
```

## First Time Using the App

1. **Create a Task**
   - Click "Tasks" tab
   - Click "New Task"
   - Enter a task like "Learn AI concepts"
   - Watch the AI suggestion appear automatically! 🤖

2. **Take a Note**
   - Click "Notes" tab
   - Write a detailed note about something you learned
   - The AI will summarize it for you

3. **Log Your Productivity**
   - Click "Productivity" tab
   - Click "Log Today"
   - Record your mood, focus level, and hours worked

4. **Get AI Insights**
   - Click "Insights" tab
   - Click "Generate Insights"
   - Get personalized recommendations based on your data

## Troubleshooting

### Backend won't start?
```bash
# Kill process on port 5000
# macOS/Linux:
kill -9 $(lsof -t -i:5000)

# Windows:
netstat -ano | findstr :5000
taskkill /PID <PID> /F
```

### Frontend can't connect?
1. Make sure backend is running
2. Check that port 5000 is accessible
3. Look in browser console (F12) for errors

### API key not working?
1. Double-check the API key is correct
2. Make sure it's in the `.env` file (NOT in .env.example)
3. Restart the backend after adding the key

## Project Structure Explained

```
ai-personal-tool/
├── backend/           ← Node.js server (port 5000)
│   └── server.js      ← All API endpoints here
├── frontend/          ← React app (port 3000)
│   └── src/
│       └── components/  ← UI sections
└── README.md          ← Full documentation
```

## Next Steps for Your CS Project

✅ This project demonstrates:
- Full-stack development
- API design and REST principles
- Database design and SQL
- Frontend-backend communication
- AI/LLM integration
- Responsive UI design

📊 **Portfolio talking points:**
- "Built a full-stack productivity app with React and Node.js"
- "Integrated Claude AI for intelligent features"
- "Designed REST API with 12+ endpoints"
- "Implemented SQLite database with 3 tables"
- "Deployed with Docker and docker-compose"

🎓 **For interviews:**
- Be ready to explain the architecture
- Discuss why you chose React and Node.js
- Explain how you integrate with the Claude API
- Talk about database schema design
- Mention performance optimizations you could add

## Deployment Checklist

Before pushing to GitHub:

- [ ] Remove API keys from code
- [ ] Create `.env.example` files
- [ ] Update README with your info
- [ ] Add a nice screenshot to README
- [ ] Tag initial version (v1.0.0)
- [ ] Write a good project description

## GitHub Instructions

```bash
# Initialize git (if not already)
git init

# Add files
git add .

# Create first commit
git commit -m "Initial commit: AI Personal Assistant full-stack app"

# Add remote (create repo on GitHub first)
git remote add origin https://github.com/yourname/ai-personal-assistant.git

# Push to GitHub
git branch -M main
git push -u origin main
```

## Getting Help

- 📚 Check the main README.md for detailed docs
- 🐛 Check browser console (F12) for errors
- 📝 API responses are logged to terminal
- 🔍 Use VS Code debugger for frontend code

---

**Happy coding! This is a great CS project! 🚀**
