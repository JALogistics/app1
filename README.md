# AI-Powered Logistics Management Platform

A secure, AI-powered logistics management platform for remote teams. It provides comprehensive features for project tracking, distribution oversight, sales insights, and an executive dashboard.

![JA Solar Logistics Platform](https://placeholder.com/wp-content/uploads/2018/10/placeholder.com-logo1.png)

## Technology Stack

- **Frontend**: Next.js 14 (App Router, Server Components, SSR)
- **Styling**: TailwindCSS
- **Backend/Database**: Supabase (Auth, PostgreSQL, Edge Functions)
- **AI Functionality**: intelligent summaries, forecasts, and insights
- **Type Safety**: TypeScript
- **Data Processing**: XLSX.js for Excel file handling

## Features

- **Project Reporting** - View all active and completed projects, upload/update project status
- **Distribution Report** - Upload and manage distribution files (CSV, XLSX)
- **Sales Reporting** - Track and analyze sales data
- **Dashboard** - Executive overview with AI-powered insights
- **File Validation** - Automatically validate uploaded files against required schemas
- **Data Consolidation** - Combine multiple data sources for comprehensive reporting

## Getting Started

### Prerequisites

- Node.js 18.x or higher
- npm or yarn
- Supabase account and project

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/logistics-platform.git
   cd logistics-platform
   ```

2. Install dependencies:
   ```bash
   npm install
   # or
   yarn install
   ```

3. Configure environment variables:
   ```bash
   cp .env.example .env.local
   ```
   Then edit `.env.local` with your Supabase credentials.

4. Run the development server:
   ```bash
   npm run dev
   # or
   yarn dev
   ```

## Docker Deployment

### Prerequisites

- Docker 20.x or higher
- Docker Compose 2.x or higher
- Supabase account and project credentials

### Building and Running with Docker

1. Create environment file:
   ```bash
   cp .env.example .env
   ```
   Edit `.env` with your Supabase credentials:
   ```env
   NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
   ```

2. Build and run with Docker Compose:
   ```bash
   docker-compose up -d
   ```

3. Access the application:
   - Open your browser at `http://localhost:3000`
   - Login with credentials: username `user1`, password `P@$$word`

### Docker Commands

Build the image:
```bash
docker-compose build
```

Run in detached mode:
```bash
docker-compose up -d
```

View logs:
```bash
docker-compose logs -f
```

Stop the container:
```bash
docker-compose down
```

Rebuild after code changes:
```bash
docker-compose up -d --build
```

### Manual Docker Commands (without Docker Compose)

Build the image:
```bash
docker build -t reporting-app .
```

Run the container (Next.js only, without Nginx):
```bash
docker run -p 3000:3000 \
  -e NEXT_PUBLIC_SUPABASE_URL=your_supabase_url \
  -e NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_key \
  reporting-app
```


## Authentication


## Project Structure

```
/
├── app/                  # Next.js App Router structure
│   ├── login/            # Authentication pages
│   ├── dashboard/        # Executive dashboard
│   ├── project-reporting/# Project management
│   ├── distribution-report/ # Distribution management
│   └── sales-reporting/  # Sales data analysis
├── components/           # Reusable UI components
│   ├── ui/               # Base UI components
│   └── logistics/        # Domain-specific components
├── lib/                  # Utility functions and hooks
├── public/               # Static assets
└── types/                # TypeScript type definitions
```

## Database Schema

The application uses a PostgreSQL database hosted on Supabase with tables for projects, distribution data, and sales information. The main table structure for daily reporting is:


```

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- JA Solar GmbH for project requirements and inspiration
- The Supabase team for their excellent database and authentication services
- Vercel for Next.js and deployment infrastructure