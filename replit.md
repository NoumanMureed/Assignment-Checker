# EduCheck - Academic Assignment Management System

## Overview

EduCheck is a full-stack web application designed for academic institutions to manage assignments, submissions, and grading with built-in plagiarism detection. The system provides separate interfaces for professors and students, enabling assignment creation, file submissions, automated similarity checking, and comprehensive grading workflows.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Build Tool**: Vite for fast development and optimized builds
- **UI Framework**: Shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with CSS custom properties for theming
- **State Management**: TanStack Query (React Query) for server state management
- **Routing**: Wouter for lightweight client-side routing
- **Form Handling**: React Hook Form with Zod validation

### Backend Architecture
- **Runtime**: Node.js with Express.js framework
- **Language**: TypeScript with ES modules
- **Database ORM**: Drizzle ORM with PostgreSQL dialect
- **Database Provider**: Neon Database (@neondatabase/serverless)
- **File Upload**: Multer for multipart form handling
- **Session Management**: Express sessions with PostgreSQL store

### Project Structure
- **Monorepo Design**: Shared schema and types between client and server
- **Client**: React application in `/client` directory
- **Server**: Express API in `/server` directory  
- **Shared**: Common schema definitions in `/shared` directory

## Key Components

### Database Schema (shared/schema.ts)
- **Users**: Stores professor and student accounts with role-based access
- **Assignments**: Assignment metadata including due dates, points, and original content
- **Submissions**: Student file submissions with extracted text content
- **Grades**: Detailed grading rubric with feedback and individual criteria scores

### Authentication & Authorization
- **Role-based Access**: Separate interfaces for professors and students
- **Session Management**: Server-side sessions with PostgreSQL persistence
- **Route Protection**: Role-specific API endpoints and UI components

### File Processing Pipeline
- **Upload Handling**: Multer middleware with file type validation (PDF, DOCX, TXT)
- **Text Extraction**: Server-side content extraction from uploaded files
- **Storage Strategy**: File metadata stored in database, content extracted to text

### Plagiarism Detection
- **Similarity Algorithm**: Word-based comparison between submissions and original content
- **Scoring System**: Percentage-based similarity scores
- **Flagging System**: Automatic flagging of high-similarity submissions

## Data Flow

### Assignment Creation (Professor)
1. Professor uploads original assignment file through drag-and-drop interface
2. Server extracts text content using file processing pipeline
3. Assignment metadata and extracted content stored in database
4. Assignment becomes available to students

### Submission Process (Student)
1. Student selects assignment and uploads their work
2. Server validates file type and extracts text content
3. Plagiarism detection compares submission against original content
4. Submission stored with similarity score and flagged status

### Grading Workflow (Professor)
1. Professor reviews submissions through grading modal interface
2. Rubric-based scoring across multiple criteria (content, structure, analysis, grammar)
3. Written feedback and total score calculation
4. Grade persistence and student notification

## External Dependencies

### UI & Interaction
- **Radix UI**: Accessible component primitives
- **Lucide React**: Icon library
- **React Dropzone**: File upload interface
- **Date-fns**: Date manipulation utilities

### Development Tools
- **ESBuild**: Fast JavaScript bundling for production
- **TSX**: TypeScript execution for development
- **Drizzle Kit**: Database migration and schema management

### Database & Storage
- **Neon Database**: Serverless PostgreSQL hosting
- **Connect PG Simple**: PostgreSQL session store adapter

## Deployment Strategy

### Development Environment
- **Vite Dev Server**: Hot module replacement and fast refresh
- **Concurrent Development**: Client and server run simultaneously
- **Replit Integration**: Cartographer plugin for Replit environment support

### Production Build
- **Client**: Vite builds optimized static assets to `/dist/public`
- **Server**: ESBuild bundles Node.js application to `/dist`
- **Database**: Drizzle manages schema migrations and deployments
- **Environment**: Production configuration through environment variables

### Key Environment Variables
- `DATABASE_URL`: PostgreSQL connection string for Neon database
- `NODE_ENV`: Environment mode (development/production)

The application follows a modern full-stack architecture with clear separation of concerns, type safety throughout the stack, and production-ready deployment capabilities.