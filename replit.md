# Budget Management System - UCAD/ESP

## Overview

This is a budget management system designed for UCAD/ESP (Université Cheikh Anta Diop / École Supérieure Polytechnique) that automates budget consolidation from departmental needs into a comprehensive budget proposal. The system supports the entire budget lifecycle from departmental input to final validation and analysis.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Full-Stack Architecture
The application follows a modern full-stack architecture pattern:
- **Frontend**: React with TypeScript using Vite for development
- **Backend**: Node.js with Express.js server
- **Database**: PostgreSQL with Drizzle ORM
- **Styling**: Tailwind CSS with shadcn/ui components
- **Authentication**: Session-based with bcrypt for password hashing

### Technology Stack
- **Frontend Framework**: React 18 with TypeScript
- **Build Tool**: Vite with HMR support
- **Backend Framework**: Express.js with TypeScript
- **Database**: PostgreSQL (configured for Neon serverless)
- **ORM**: Drizzle ORM with migrations
- **UI Components**: shadcn/ui built on Radix UI primitives
- **Styling**: Tailwind CSS with custom UCAD branding
- **State Management**: TanStack Query for server state
- **Form Handling**: React Hook Form with Zod validation
- **Authentication**: Express sessions with bcrypt

## Key Components

### Database Schema
The system uses a comprehensive schema with the following main entities:
- **users**: User accounts with role-based access (user, chef_dept, direction, comptable)
- **budgetCategories**: Budget nomenclature codes (recette/depense types)
- **budgetLines**: Individual budget line items with approval workflow
- **budgetHistory**: Audit trail for budget changes
- **budgetReports**: Generated budget reports

### User Roles & Permissions
- **User**: Basic department members who can create budget entries
- **Chef_dept**: Department heads who can consolidate departmental budgets
- **Direction**: Directors who can modify and validate final budget
- **Comptable**: Accounting staff with read-only access for analysis

### Budget Workflow
1. **Draft**: Initial budget entry by users
2. **Pending**: Submitted for departmental review
3. **Validated**: Approved by department head
4. **Rejected**: Rejected with reason
5. **Consolidated**: Final consolidated budget

### Frontend Architecture
- **Pages**: Dashboard, Budget Entry, Consolidation, Analysis, Reports, History
- **Components**: Reusable UI components with consistent styling
- **Hooks**: Custom hooks for authentication and data fetching
- **Routing**: Client-side routing with wouter
- **Forms**: Validated forms with proper error handling

### API Structure
RESTful API endpoints organized by feature:
- `/api/auth/*`: Authentication endpoints
- `/api/budget-lines/*`: Budget line CRUD operations
- `/api/budget-categories/*`: Budget category management
- `/api/consolidation/*`: Budget consolidation workflow
- `/api/budget-analysis/*`: Budget analysis and reporting
- `/api/reports/*`: Report generation

## Data Flow

### Budget Entry Process
1. User selects budget category from nomenclature
2. Enters proposed amount and description
3. Form validation ensures data integrity
4. Budget line created with "draft" status
5. User can submit for departmental review (status: "pending")

### Consolidation Workflow
1. Department heads view pending budget lines
2. Can validate, reject, or request modifications
3. Validated lines move to "validated" status
4. Direction can review and modify final budget
5. Final consolidation creates comprehensive budget document

### Analysis & Reporting
1. System calculates variances between proposed and realized amounts
2. Generates summary statistics and trend analysis
3. Provides filtering and search capabilities
4. Exports reports in various formats (Excel, PDF planned)

## External Dependencies

### Core Dependencies
- **@neondatabase/serverless**: PostgreSQL database connection
- **drizzle-orm**: Type-safe database queries
- **@tanstack/react-query**: Server state management
- **react-hook-form**: Form handling
- **zod**: Schema validation
- **bcrypt**: Password hashing
- **express-session**: Session management

### UI Dependencies
- **@radix-ui/***: Accessible UI primitives
- **tailwindcss**: Utility-first CSS framework
- **lucide-react**: Icon library
- **class-variance-authority**: Utility for component variants

### Development Dependencies
- **vite**: Build tool and dev server
- **typescript**: Type checking
- **tsx**: TypeScript execution
- **esbuild**: Production bundling

## Deployment Strategy

### Development Environment
- Vite dev server for frontend with HMR
- Express server with TypeScript compilation
- Database migrations with Drizzle Kit
- Session storage with environment variables

### Production Build
- Frontend built with Vite and served statically
- Backend bundled with esbuild
- PostgreSQL database (Neon serverless recommended)
- Environment-based configuration

### Database Management
- Schema defined in shared/schema.ts
- Migrations managed with Drizzle Kit
- Connection pooling with Neon serverless
- Backup strategy should be implemented

### Security Considerations
- Session-based authentication with secure cookies
- Password hashing with bcrypt
- SQL injection prevention through Drizzle ORM
- Role-based access control
- Input validation with Zod schemas

### Scalability Notes
- Stateless backend design for horizontal scaling
- Database connection pooling
- Client-side caching with TanStack Query
- Optimistic updates for better UX

The system is designed to be maintainable, scalable, and secure while providing a comprehensive budget management solution for academic institutions.