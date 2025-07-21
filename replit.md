# 7loww - Order Management System

## Overview

7loww is a full-stack order management platform connecting sellers and customers with real-time updates. Built with React, Express.js, PostgreSQL, and Replit authentication. The system provides inventory management with kg-based pricing, seller dashboards, public order forms, and dark mode support.

## User Preferences

Preferred communication style: Simple, everyday language.
App name: "7loww" (changed from OrderFlow)
Single seller application - no landing page or "get started" sections
Order form is the main public page (/) - seller shares this link on socials
Seller dashboard behind authentication (/dashboard)
Dark mode functionality required
Inventory management with kg-based pricing for automatic form population
Design inspiration: Square Dashboard and Shopify Orders interface
Authentication: Replit Auth integration with seller profiles

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **UI Components**: shadcn/ui component library built on Radix UI primitives
- **Styling**: Tailwind CSS with custom design tokens and CSS variables
- **State Management**: TanStack Query (React Query) for server state management
- **Routing**: Wouter for client-side routing
- **Forms**: React Hook Form with Zod validation
- **Build Tool**: Vite with custom configuration for development and production

### Backend Architecture
- **Runtime**: Node.js with Express.js framework
- **Language**: TypeScript with ES modules
- **API Style**: RESTful API with WebSocket support for real-time updates
- **Validation**: Zod schemas for request/response validation
- **Error Handling**: Centralized error middleware with structured error responses

### Real-time Communication
- **WebSocket Server**: Built-in WebSocket server for live order updates
- **Event Broadcasting**: Real-time notifications for order status changes, new orders, and deletions
- **Connection Management**: Automatic reconnection and connection status monitoring

## Key Components

### Database Layer
- **ORM**: Drizzle ORM with PostgreSQL dialect
- **Database Provider**: Neon serverless PostgreSQL (configured via `@neondatabase/serverless`)
- **Schema Management**: Centralized schema definitions in `shared/schema.ts`
- **Migrations**: Drizzle Kit for database migrations and schema changes

### Data Models
- **Users Table**: Seller profiles with business information and authentication data
- **Products Table**: Inventory management with kg-based pricing, categories, and seller relationships
- **Orders Table**: Customer orders linked to sellers with item details and status tracking
- **Sessions Table**: Authentication session storage for Replit Auth
- **Schema Validation**: Zod schemas for type-safe data validation
- **Decimal Precision**: Proper decimal handling for monetary values

### Authentication System
- **Provider**: Replit OpenID Connect authentication
- **Session Management**: PostgreSQL-backed session storage
- **User Profiles**: Business information, contact details, and profile images
- **Authorization**: Protected routes for seller dashboard and inventory management

### Storage Implementation
- **Interface**: `IStorage` interface for database operations
- **Implementation**: `DatabaseStorage` with full PostgreSQL integration
- **Operations**: User management, product CRUD, order processing, and real-time updates

### Frontend Components
- **Dashboard**: Order overview with statistics and real-time updates
- **Order Form**: Multi-step order creation with validation
- **Orders Table**: Sortable, filterable order listing with actions
- **Statistics Cards**: Real-time metrics display
- **UI Components**: Comprehensive component library (buttons, forms, dialogs, etc.)

## Data Flow

1. **Order Creation**: Form submission → validation → API call → database insert → WebSocket broadcast
2. **Order Updates**: Status change → API call → database update → WebSocket notification → UI refresh
3. **Real-time Updates**: WebSocket messages → React Query invalidation → automatic UI updates
4. **Search/Filter**: Query parameters → API request → filtered results → table update

## External Dependencies

### Core Dependencies
- **@neondatabase/serverless**: PostgreSQL database connection
- **drizzle-orm**: Database ORM and query builder
- **@tanstack/react-query**: Server state management
- **@radix-ui/***: Accessible UI primitives
- **react-hook-form**: Form state management
- **zod**: Runtime type validation
- **wouter**: Lightweight routing
- **ws**: WebSocket implementation

### Development Tools
- **drizzle-kit**: Database migration tool
- **vite**: Build tool and development server
- **typescript**: Type checking and compilation
- **tailwindcss**: Utility-first CSS framework
- **tsx**: TypeScript execution for development

## Deployment Strategy

### Build Process
- **Frontend**: Vite builds React app to `dist/public`
- **Backend**: esbuild bundles server code to `dist/index.js`
- **Assets**: Static file serving through Express in production

### Environment Configuration
- **Database**: PostgreSQL connection via `DATABASE_URL` environment variable
- **Development**: Hot module replacement with Vite middleware
- **Production**: Optimized builds with static file serving

### Scripts
- `dev`: Development server with hot reload
- `build`: Production build for both frontend and backend
- `start`: Production server startup
- `db:push`: Database schema deployment

### Database Setup
- Drizzle configuration for PostgreSQL dialect
- Migration files generated in `./migrations` directory
- Schema definitions shared between frontend and backend
- Environment-based database URL configuration

The application follows a modern full-stack architecture with strong typing, real-time capabilities, and a focus on developer experience through hot reloading and type safety.