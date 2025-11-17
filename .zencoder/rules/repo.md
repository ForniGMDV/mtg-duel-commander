---
description: Repository Information Overview
alwaysApply: true
---

# Repository Information Overview

## Repository Summary
Magic: The Gathering Duel Commander - AI Bot is a full-stack monorepo application featuring a React frontend, Node.js/Express backend, and Python FastAPI AI service. The project implements complete MTG Duel Commander rules with real-time gameplay via WebSocket, AI-powered bot using Monte Carlo Tree Search, and self-play training capabilities.

## Repository Structure
```
bettermtgbot/
├── frontend/           # React + TypeScript UI (Vite, Tailwind CSS, Pixi.js)
├── backend/            # Node.js + Express API (TypeScript, WebSocket)
├── ai/                 # Python FastAPI AI service (PyTorch, MCTS)
├── shared/             # Game engine & shared types
├── node_modules/       # Root workspace dependencies
├── .env.example        # Environment configuration template
├── package.json        # Root workspace configuration
├── dev.ps1            # Development startup script
└── README.md          # Project documentation
```

### Main Repository Components
- **Frontend**: React 18 UI with Zustand state management, Pixi.js board rendering, and Tailwind CSS styling
- **Backend**: Express.js REST API with Socket.io real-time communication, Mongoose/Sequelize ORM support, and caching
- **AI Service**: FastAPI framework with PyTorch neural networks and MCTS decision-making
- **Shared**: TypeScript-based game engine and type definitions used across projects

## Projects

### Frontend (mtg-duel-frontend)
**Configuration File**: `frontend/package.json`

#### Language & Runtime
**Language**: TypeScript 5.3+
**Runtime**: Node.js 18+
**Build System**: Vite 5.0
**Package Manager**: npm

#### Dependencies
**Main Dependencies**:
- React 18.2, React DOM 18.2
- React Router DOM 6.20
- Zustand 4.4 (state management)
- Pixi.js 8.0 (board rendering)
- Framer Motion 12.23 (animations)
- Socket.io-client 4.7.2 (real-time communication)
- Axios 1.13 (HTTP client)

**Development Dependencies**:
- Vite 5.0, @vitejs/plugin-react 4.2
- Tailwind CSS 3.3, PostCSS 8.4, Autoprefixer 10.4
- ESLint 8.50, @typescript-eslint plugins
- Typescript 5.3

#### Build & Installation
```bash
cd frontend
npm install
npm run dev        # Start dev server (port 5173)
npm run build      # Production build
npm run lint       # Run ESLint
npm run preview    # Preview production build
```

#### Vite Configuration
- Dev server on port 5173
- API proxy to backend (`/api` → `http://localhost:3001`)
- React plugin for JSX/TSX support

#### Entry Points
- `src/main.tsx`: Application entry point
- `src/App.tsx`: Main application component
- `src/pages/GamePage.tsx`: Primary game interface (50KB)
- `src/components/GameBoard.jsx`: Game board rendering

### Backend (mtg-duel-backend)
**Configuration File**: `backend/package.json`

#### Language & Runtime
**Language**: TypeScript 5.3+
**Runtime**: Node.js 18+
**Build System**: TypeScript compiler
**Package Manager**: npm
**Module System**: ES2020 (ESM)

#### Dependencies
**Main Dependencies**:
- Express 4.18.2 (REST framework)
- Socket.io 4.7.2 (WebSocket server)
- Mongoose 7.5 (MongoDB ODM)
- Sequelize 6.34, PostgreSQL (pg 8.11)
- Axios 1.6 (HTTP client)
- CORS 2.8.5, dotenv 16.3
- node-cache 5.1.2, uuid 9.0.0

**Development Dependencies**:
- Nodemon 3.0 (auto-restart)
- tsx 4.20.6, ts-node 10.9 (TypeScript execution)
- ESLint 8.50, @typescript-eslint plugins
- Typescript 5.3

#### TypeScript Configuration
- Target: ES2020, Module: ES2020
- Strict mode enabled
- Path aliases configured (@/, @routes/, @services/, @models/, etc.)
- Source maps and declaration files enabled

#### Build & Installation
```bash
cd backend
npm install
npm run dev        # Start with nodemon (auto-reload)
npm run build      # Compile TypeScript → dist/
npm run start      # Run compiled JS (dist/index.js)
npm run lint       # Run ESLint
npm run typecheck  # Type checking without emit
```

#### Entry Points
- `src/index.ts`: Main server entry point
- `src/routes/api.js`: API routes
- `src/routes/gameRoutes.ts`: Game-specific endpoints
- `src/game-engine/engine.js`: Core game engine (9.14 KB)
- `src/game-engine/rulesEngine.js`: Rules enforcement (22.41 KB)

#### Core Game Components
- **Game Engine**: Core game mechanics and state management
- **Rules Engine**: MTG Duel Commander rule validation
- **Card Effects**: Card ability implementations (27.31 KB)
- **Advanced Bot**: AI decision logic and strategy (19.09 KB)
- **Training System**: Self-play simulation framework (32.21 KB)
- **Deck Import Service**: Scryfall integration for deck importing
- **Game Socket**: WebSocket event handlers

### AI Service (Python)
**Configuration File**: `ai/requirements.txt`

#### Language & Runtime
**Language**: Python 3.10+
**Framework**: FastAPI 0.104.0
**Server**: Uvicorn 0.24.0
**Package Manager**: pip

#### Dependencies
**Core Dependencies**:
- FastAPI 0.104.0 (API framework)
- Uvicorn 0.24.0 (ASGI server)
- PyTorch 2.0+ (neural networks)
- NumPy 1.24+, Pandas 2.0+ (data processing)
- TensorBoard 2.14 (monitoring)

**Additional Libraries**:
- Pydantic 2.4 (data validation)
- python-dotenv 1.0 (configuration)
- Requests 2.31 (HTTP client)
- python-multipart 0.0.6 (form handling)
- aiofiles 23.2 (async file operations)

#### Build & Installation
```bash
cd ai
python -m venv venv
venv\Scripts\activate              # Windows
source venv/bin/activate           # macOS/Linux
pip install -r requirements.txt
python -m src.main                 # Run server
```

#### Entry Points
- `ai/src/main.py`: FastAPI application entry point

### Shared Library
**Location**: `shared/`

**Components**:
- `game-engine/game-engine.ts`: Shared game logic (2.27 KB)
- `game-engine/stack.ts`: Game stack management (533 B)
- `types/game.ts`: TypeScript game type definitions (1.7 KB)

## Root Workspace Configuration

**Package Manager**: npm workspaces
**Workspaces**: frontend, backend, ai

**Root Scripts**:
```bash
npm run dev              # Start all services (PowerShell: dev.ps1)
npm run stop-dev        # Stop all services (PowerShell: stop-dev.ps1)
npm run dev:workspaces  # Run dev for all workspaces
npm run build           # Build all workspaces
npm run lint            # Lint all workspaces
npm run test            # Test all workspaces
```

## Configuration & Environment

**.env.example** defines:
- `NODE_ENV`: development
- `PORT`: 3001 (backend API)
- `AI_PORT`: 3002 (Python service)
- `DATABASE_URL`: PostgreSQL connection string
- `MONGODB_URL`: MongoDB connection string
- `JWT_SECRET`: Authentication secret
- `JWT_EXPIRATION`: 7d
- `SCRYFALL_API_URL`: MTG card API

## API Architecture

**Game Endpoints**:
- POST /api/games - Create new game
- GET /api/games/:id - Get game state
- POST /api/games/:id/action - Execute action

**WebSocket Events**:
- game:start, game:action, game:state-update, game:end

**Frontend Dev Server**: http://localhost:5173
**Backend API Server**: http://localhost:3001
**AI Service Server**: Configured via AI_PORT (typically 3002)

## Key Technologies
- **Frontend**: React 18, TypeScript, Vite, Zustand, Tailwind CSS, Pixi.js
- **Backend**: Node.js/Express, TypeScript, Socket.io, Mongoose, Sequelize
- **AI**: Python, FastAPI, PyTorch, MCTS
- **Database**: PostgreSQL (user data), MongoDB (AI training data)
- **Real-time**: WebSocket via Socket.io
