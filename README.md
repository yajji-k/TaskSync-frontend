# TaskSync Frontend

TaskSync-frontend is the Angular-based frontend for a real-time collaborative task management system, designed to demonstrate senior-level software engineering skills (SWE2). Built with Angular and TypeScript, it provides a responsive user interface with a Kanban board, task management forms, and real-time updates via WebSocket, integrating seamlessly with the TaskSync-backend (Spring Boot microservices). The project emphasizes modern frontend practices, API integration, and modularity, serving as a portfolio piece for enterprise-grade web development. Future plans include extending to a React Native mobile app.

## Table of Contents
- [Project Overview](#project-overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Frontend Architecture](#frontend-architecture)
- [Setup Instructions](#setup-instructions)
- [Integration with Backend](#integration-with-backend)
- [Deployment](#deployment)
- [Testing](#testing)
- [Future Enhancements](#future-enhancements)
- [License](#license)

## Project Overview
TaskSync is a web-based task management tool inspired by Trello and Asana, enabling users to create, assign, and manage tasks collaboratively in real time. This repository contains the Angular frontend, which integrates with the TaskSync-backend (a monorepo of Spring Boot microservices for authentication, task management, and WebSocket notifications). The frontend showcases SWE2-level skills in building responsive UIs, consuming REST APIs, and handling real-time updates, with a modular design to support future mobile app development.

## Features
- **User Authentication**: Login/register via email/password or Google OAuth, with secure token management.
- **Task Management**: Create, edit, delete, and assign tasks with statuses (To-Do, In Progress, Done) via forms.
- **Real-Time Collaboration**: Display task updates instantly using WebSocket (STOMP).
- **Kanban Board**: Visualize tasks with drag-and-drop functionality for status updates.
- **Dashboard**: View tasks in list or board view with filters (status, assignee) and a chart showing task status distribution.
- **Responsive Design**: Mobile-friendly UI with Angular Material or Bootstrap.

## Tech Stack
- **Frontend**: Angular (TypeScript), Angular Material or Bootstrap (styling), ng2-charts (visualizations), ngx-dnd or similar (drag-and-drop), stompjs or ngx-socket-io (WebSocket).
- **Tools**: Node.js, npm (dependency management), GitHub (version control), Postman (API testing).
- **Deployment**: Netlify or Vercel (frontend).

## Frontend Architecture
The frontend is organized as an Angular project with modular components and services:
- **Components**:
  - `LoginComponent`: Handles user authentication (email/password, Google OAuth).
  - `TaskFormComponent`: Form for creating/editing tasks.
  - `TaskBoardComponent`: Kanban board for task visualization and drag-and-drop.
  - `DashboardComponent`: Displays tasks and status chart.
- **Services**:
  - `AuthService`: Manages login, token storage, and user role handling.
  - `TaskService`: Handles task CRUD operations via REST APIs.
  - `WebSocketService`: Connects to WebSocket for real-time updates.
- **Project Structure**:
  ```
  /task-sync-frontend
  ├── /src
  │   ├── /app
  │   │   ├── /components
  │   │   │   ├── login
  │   │   │   ├── task-form
  │   │   │   ├── task-board
  │   │   │   ├── dashboard
  │   │   ├── /services
  │   │   │   ├── auth.service.ts
  │   │   │   ├── task.service.ts
  │   │   │   ├── websocket.service.ts
  │   ├── /assets
  │   ├── /styles
  ├── /docs                # Documentation
  ├── /deploy             # Deployment scripts
  ├── README.md
  ```

## Setup Instructions
### Prerequisites
- Node.js 18+
- Angular CLI 17+
- TaskSync-backend (running locally or deployed)
- Google OAuth credentials (for SSO)

### Steps
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/task-sync-frontend.git
   cd task-sync-frontend
   ```

2. **Install Dependencies**:
   ```bash
   npm install
   ```

3. **Configure Environment Variables**:
   - Update `src/environments/environment.ts` and `environment.prod.ts` with backend API and WebSocket URLs:
     ```typescript
     export const environment = {
       production: false,
       apiUrl: 'http://localhost:8080/api',
       wsUrl: 'http://localhost:8080/ws'
     };
     ```

4. **Run the Application**:
   - Start the Angular development server:
     ```bash
     ng serve
     ```
   - Access the app at `http://localhost:4200`.

5. **Verify Setup**:
   - Test login functionality with email/password or Google OAuth.
   - Verify task creation and real-time updates via Postman or browser.

## Integration with Backend
The frontend integrates with the TaskSync-backend microservices:
- **Auth Service**:
  - `POST /api/auth/register`: Register a new user.
  - `POST /api/auth/login`: Login and receive JWT.
  - `GET /api/auth/google`: Google OAuth login.
- **Task Service**:
  - `POST /api/tasks`: Create a task.
  - `GET /api/tasks`: List tasks (filtered by user/status).
  - `PUT /api/tasks/{id}`: Update a task.
  - `DELETE /api/tasks/{id}`: Delete a task.
- **WebSocket Service**:
  - Connect to `/ws` endpoint (STOMP over WebSocket).
  - Subscribe to events: `task.created`, `task.updated`, `task.deleted`.

## Deployment
1. **Build for Production**:
   ```bash
   ng build --prod
   ```
2. **Deploy**:
   - Deploy the `dist` folder to Netlify or Vercel.
   - Configure environment variables for backend API and WebSocket URLs.
3. **Verify**:
   - Test the deployed app for authentication, task management, and real-time updates.

## Testing
- Unit tests for components (`LoginComponent`, `TaskFormComponent`, etc.) using Jasmine/Karma.
- Unit tests for services (`AuthService`, `TaskService`, `WebSocketService`).
- End-to-end tests for user flows: login, task creation, drag-and-drop, real-time updates.

## Future Enhancements
- **Mobile App**: Develop a React Native app to reuse backend APIs and WebSocket, with push notifications for mobile access.
- **AI Integration**: Consume a future Python FastAPI microservice for AI-driven features (e.g., task prioritization, NLP categorization) via REST or gRPC.
