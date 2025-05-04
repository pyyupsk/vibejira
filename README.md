# VibeJira

A web application to display and interact with JIRA tickets.

## Overview

This project is organized as a [Turborepo](https://turborepo.org) monorepo with the following structure:

- **Backend (`apps/backend/`)**: A Node.js/Express application that connects to the JIRA REST API using a Personal Access Token (PAT) to fetch and manipulate ticket data.
- **Frontend (`apps/frontend/`)**: A React application built with Create React App and CoreUI v5 for the user interface. It communicates with the backend API.

## Prerequisites

- Node.js (v16 or later recommended)
- npm (usually comes with Node.js)
- A JIRA Cloud instance
- A JIRA Personal Access Token (PAT) - See [Atlassian Documentation](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/) on how to create one. You'll need permissions to read/write JIRA issues.

## Setup

### Root Setup

1. **Clone the repository:**

```bash
git clone git@github.com:thananon/vibejira.git
cd vibejira
```

2. **Install dependencies:**

```bash
npm install
```

### Backend Setup (`apps/backend/`)

1. **Create a `.env` file:**

   Create a file named `.env` in the `apps/backend/` directory and add the following variables, replacing the placeholder values with your actual JIRA information:

   ```dotenv
   # Backend server port
   PORT=3001

   # Your JIRA Cloud instance base URL
   JIRA_BASE_URL=https://your-domain.atlassian.net

   # Your JIRA Personal Access Token (PAT)
   JIRA_PAT=your_jira_personal_access_token_here

   # Frontend URL (for CORS)
   FRONTEND_ORIGIN=http://localhost:3000

   # Optional for debugging
   JIRA_API_DEBUG=false
   ```

### Frontend Setup (`apps/frontend/`)

No additional configuration is needed for the frontend as it's set up to connect to the backend automatically.

## Running the Application

### Development Mode

From the root directory, you can run both frontend and backend simultaneously using:

```bash
npm run dev
```

This will start:

- Backend server at `http://localhost:3001`
- Frontend development server at `http://localhost:3000`

### Running Individual Services

If you need to run the services separately:

1. **Backend only:**

```bash
turbo run dev --filter=backend
```

2. **Frontend only:**

```bash
turbo run dev --filter=frontend
```

3. **Backend with debugging enabled:**

```bash
turbo run debug --filter=backend
```

## Building for Production

To build all applications:

```bash
npm run build
```

This will create production builds for both the frontend and backend.

## Project Structure

```
.
├── apps/
│   ├── frontend/         # React frontend application
│   │   ├── public/
│   │   ├── src/
│   │   └── package.json
│   └── backend/          # Express backend server
│       ├── src/
│       └── package.json
├── turbo.json            # Turborepo configuration
└── package.json          # Root package.json
```

## Turborepo Features

This project uses Turborepo for:

- Optimized build caching
- Parallel task execution
- Dependency graph management
- Standardized scripts across packages

## Adding New Workspace Packages

To add a new package to the monorepo:

1. Create a new directory in `apps/` or `packages/`
2. Initialize it with `npm init`
3. Add the appropriate scripts (dev, build, test, etc.)
4. The package will automatically be included in the workspace

**Note:** The frontend currently uses mock data. Integration with the backend API endpoints is the next step.
