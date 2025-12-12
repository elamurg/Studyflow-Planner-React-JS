# StudyFlow - Time Blocking Calendar for Students

A modern study planner application with a drag-and-drop calendar, deadline countdowns, progress tracking, and notes for future study sessions.

![StudyFlow](https://img.shields.io/badge/StudyFlow-Study%20Smarter-8B5CF6)
![React](https://img.shields.io/badge/React-18.3-61DAFB?logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6?logo=typescript)
![Flask](https://img.shields.io/badge/Flask-3.0-000000?logo=flask)
![TailwindCSS](https://img.shields.io/badge/Tailwind-3.4-06B6D4?logo=tailwindcss)

## Features

- **Time Block Calendar** - Drag-and-drop study sessions on a weekly calendar view
- **Deadline Tracker** - Set deadlines with live countdown timers
- **Progress Tracking** - Checklist of study items with completion progress
- **Notes** - Leave notes for your future self for upcoming study sessions
- **Class Organization** - Organize everything by subject/class with color coding
- **Persistent Storage** - All data saved to database, syncs across devices

## Screenshots

| Calendar View | Deadlines & Progress |
|---------------|---------------------|
| Drag and drop time blocks | Track deadlines with countdowns |

## Tech Stack

### Frontend
- **React 18** with TypeScript
- **Vite** for fast development and building
- **Tailwind CSS** for styling
- **shadcn/ui** + Radix UI for components
- **TanStack Query** (React Query) for data fetching
- **date-fns** for date manipulation

### Backend
- **Flask 3.0** (Python)
- **SQLAlchemy** ORM
- **SQLite** (development) / **PostgreSQL** (production)
- **Flask-CORS** for cross-origin requests
- **Gunicorn** for production server

## Project Structure

```
studyflow-planner/
├── src/                      # Frontend source
│   ├── components/           # React components
│   │   ├── ui/              # shadcn/ui components
│   │   ├── TimeBlockCalendar.tsx
│   │   ├── DeadlineCard.tsx
│   │   ├── NotesSection.tsx
│   │   └── ...
│   ├── hooks/               # Custom React hooks
│   │   └── useStudyApi.ts   # API integration hooks
│   ├── lib/                 # Utilities
│   │   └── api.ts           # API client
│   ├── pages/               # Page components
│   │   └── Index.tsx        # Main dashboard
│   ├── types/               # TypeScript types
│   │   └── study.ts         # Data type definitions
│   └── main.tsx             # App entry point
│
├── backend/                  # Backend source
│   ├── App.py               # Flask application & API routes
│   ├── requirements.txt     # Python dependencies
│   ├── Procfile            # Deployment config
│   └── .env.example        # Environment template
│
├── public/                   # Static assets
├── index.html               # HTML entry point
├── package.json             # Node dependencies
├── tailwind.config.ts       # Tailwind configuration
├── vite.config.ts           # Vite configuration
└── README.md                # This file
```

## Getting Started

### Prerequisites

- **Node.js** 18+ and npm
- **Python** 3.9+
- **Git**

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/elamurg/studyflow-planner.git
   cd studyflow-planner
   ```

2. **Set up the backend**
   ```bash
   # Create Python virtual environment
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   
   # Install Python dependencies
   pip install -r backend/requirements.txt
   
   # Create environment file
   cp backend/.env.example backend/.env
   ```

3. **Set up the frontend**
   ```bash
   # Install Node dependencies
   npm install
   
   # Create environment file
   echo "VITE_API_URL=http://localhost:5001/api" > .env
   ```

### Running Locally

You need **two terminals** - one for the backend and one for the frontend.

**Terminal 1 - Backend:**
```bash
cd backend
source ../venv/bin/activate  # On Windows: ..\venv\Scripts\activate
PORT=5001 python App.py
```
Backend runs at http://localhost:5001

**Terminal 2 - Frontend:**
```bash
npm run dev
```
Frontend runs at http://localhost:8080

Open http://localhost:8080 in your browser.

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| **Study Sessions** |
| GET | `/api/sessions` | Get all study sessions |
| POST | `/api/sessions` | Create a new session |
| PUT | `/api/sessions/:id` | Update a session |
| DELETE | `/api/sessions/:id` | Delete a session |
| **Deadlines** |
| GET | `/api/deadlines` | Get all deadlines |
| POST | `/api/deadlines` | Create a new deadline |
| PUT | `/api/deadlines/:id` | Update a deadline |
| DELETE | `/api/deadlines/:id` | Delete a deadline |
| **Study Items** |
| GET | `/api/items` | Get all checklist items |
| POST | `/api/items` | Create a new item |
| PUT | `/api/items/:id` | Update/toggle item |
| DELETE | `/api/items/:id` | Delete an item |
| GET | `/api/items/progress` | Get progress statistics |
| **Notes** |
| GET | `/api/notes` | Get all notes |
| POST | `/api/notes` | Create a new note |
| PUT | `/api/notes/:id` | Update a note |
| DELETE | `/api/notes/:id` | Delete a note |
| **Subjects** |
| GET | `/api/subjects` | Get all subjects/classes |
| POST | `/api/subjects` | Create a new subject |
| DELETE | `/api/subjects/:id` | Delete a subject |
| **Health** |
| GET | `/api/health` | Health check endpoint |

## Deployment

### Deploy Backend to Render

1. Push your code to GitHub

2. Create a [Render](https://render.com) account and connect GitHub

3. Create a **New Web Service**:
   - **Root Directory**: `backend`
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `gunicorn App:app`
   - **Instance Type**: Free

4. Add environment variables:
   | Key | Value |
   |-----|-------|
   | `FRONTEND_URL` | Your frontend URL |
   | `FLASK_DEBUG` | `False` |

5. (Optional) Add a **PostgreSQL** database for persistent storage

### Deploy Frontend to Vercel

1. Create a [Vercel](https://vercel.com) account and import your repo

2. Configure:
   - **Framework**: Vite
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`

3. Add environment variable:
   | Key | Value |
   |-----|-------|
   | `VITE_API_URL` | `https://your-backend.onrender.com/api` |

4. Deploy!

### Alternative: Deploy Frontend to Netlify

1. Create a [Netlify](https://netlify.com) account

2. Import from GitHub

3. Configure:
   - **Build Command**: `npm run build`
   - **Publish Directory**: `dist`

4. Add environment variable `VITE_API_URL`

## Environment Variables

### Frontend (.env)
```env
VITE_API_URL=http://localhost:5001/api
```

### Backend (backend/.env)
```env
DATABASE_URL=sqlite:///studyflow.db
FRONTEND_URL=http://localhost:8080
FLASK_DEBUG=True
PORT=5001
```

## Development

### Frontend Commands
```bash
npm run dev      # Start development server
npm run build    # Build for production
npm run preview  # Preview production build
npm run lint     # Run ESLint
```

### Backend Commands
```bash
python App.py              # Start development server
gunicorn App:app          # Start production server
```

### Adding New Features

1. **New API endpoint**: Add route in `backend/App.py`
2. **New React Query hook**: Add in `src/hooks/useStudyApi.ts`
3. **New component**: Add in `src/components/`
4. **New UI component**: Use `npx shadcn-ui@latest add <component>`

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [shadcn/ui](https://ui.shadcn.com/) for beautiful UI components
- [Tailwind CSS](https://tailwindcss.com/) for utility-first styling
- [Lovable](https://lovable.dev/) for initial project scaffolding
- [TanStack Query](https://tanstack.com/query) for data synchronization

---

Built with care for students, by students.