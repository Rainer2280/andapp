# AuraPoints Web Application

## Overview

AuraPoints is a "get-paid-to-watch" web application where users earn points (AuraPoints/AP) by viewing advertisements and can convert these points into real currency (Euros). The platform features a gamified experience with daily streaks, referral programs, and multiple cashout options.

**Current Status**: Fully functional with PayPal integration, user authentication, and ad watching system implemented.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Technology Stack
- **Frontend**: React with TypeScript, Vite build tool
- **Backend**: Express.js with TypeScript 
- **Database**: PostgreSQL with Drizzle ORM
- **Authentication**: Replit Auth with OpenID Connect
- **UI Framework**: Tailwind CSS with shadcn/ui components
- **State Management**: TanStack React Query for server state
- **Payment Integration**: PayPal SDK for cashouts

### Architectural Pattern
The application follows a full-stack monorepo structure with clear separation between client, server, and shared code. It uses a traditional RESTful API architecture with session-based authentication.

## Key Components

### Frontend Architecture
- **Component Structure**: Modern React with hooks and context for state management
- **Routing**: Wouter for lightweight client-side routing
- **Styling**: Tailwind CSS with custom CSS variables for theming
- **UI Components**: Radix UI primitives wrapped with shadcn/ui for consistency
- **Internationalization**: Custom context-based translation system supporting 5 languages (EN, ET, FI, DE, ES)

### Backend Architecture
- **API Layer**: Express.js with TypeScript for type safety
- **Database Layer**: Drizzle ORM for type-safe database operations
- **Authentication**: Replit Auth integration with session management
- **Session Storage**: PostgreSQL-based session store using connect-pg-simple

### Database Schema
- **Users**: Core user data with AuraPoints-specific fields (balance, streaks, referrals)
- **Ads**: Advertisement data with rewards and duration
- **Earnings**: User earning history and transaction logs
- **Cashouts**: Withdrawal requests and payment processing
- **Referrals**: Multi-level referral system tracking
- **Sessions**: Authentication session management (required for Replit Auth)

## Data Flow

### Authentication Flow
1. Users authenticate via Replit Auth (OpenID Connect)
2. Session data stored in PostgreSQL
3. Protected routes verify authentication status
4. User data synchronized between auth provider and local database

### Points System Flow
1. Users watch ads through modal interface
2. Ad completion triggers earning record creation
3. User balance updated in real-time
4. Progress tracked for streaks and bonuses

### Cashout Flow
1. Users request withdrawal when minimum threshold met (€10.00)
2. Payment details validated (PayPal/SEPA)
3. Cashout record created with pending status
4. Admin processing required for completion

## External Dependencies

### Core Dependencies
- **@neondatabase/serverless**: Neon PostgreSQL serverless driver
- **@paypal/paypal-server-sdk**: PayPal payment processing
- **@tanstack/react-query**: Server state management
- **drizzle-orm**: Type-safe database ORM
- **express**: Web application framework
- **passport**: Authentication middleware

### UI Dependencies
- **@radix-ui/***: Accessible UI primitives
- **tailwindcss**: Utility-first CSS framework
- **lucide-react**: Icon library
- **wouter**: Lightweight routing

### Development Dependencies
- **vite**: Fast build tool and dev server
- **typescript**: Type safety across the stack
- **tsx**: TypeScript execution for Node.js

## Deployment Strategy

### Build Process
- Frontend built with Vite to `dist/public`
- Backend bundled with esbuild to `dist/index.js`
- Shared schema accessible to both frontend and backend

### Environment Configuration
- Database connection via `DATABASE_URL` environment variable
- Replit Auth configuration through environment variables
- Session secret for secure cookie signing

### Production Considerations
- PostgreSQL database provisioning required
- Static file serving for production builds
- Session store configured for persistence
- HTTPS required for secure authentication

### Development Workflow
- Hot reload via Vite dev server
- TypeScript compilation checking
- Database schema management through Drizzle migrations
- Replit-specific development tooling integration