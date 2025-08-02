# GestionePro - Business Management System

## Overview

GestionePro is a comprehensive business management platform designed for companies seeking to optimize their workflow, presence management, and internal activity monitoring. The system provides role-based access control, task management, attendance tracking, and notification systems with a modern React frontend and Express.js backend architecture.

## Recent Changes - MANUAL-ONLY ATTENDANCE SYSTEM (August 1, 2025)

### Complete Removal of Automatic Clock In/Out System
- **Frontend Simplification**: Removed all clock-in/clock-out buttons and logic from AttendanceWidget
- **Backend Cleanup**: Removed `/api/attendance/clock-in`, `/api/attendance/clock-out`, and `/api/attendance/auto-clock-out` endpoints
- **Manual-Only Approach**: System now relies entirely on manual attendance entry with precise time control
- **Time Display**: Widget now shows current time with "Solo Inserimento Manuale" message
- **Simplified User Experience**: No more confusion between automatic and manual systems
- **Precise Control**: Users can specify exact working hours (07:30-12:00, 13:00-16:45) without automatic interference

## Previous Changes - VACATION CALCULATION SYSTEM COMPLETE (August 1, 2025)

### Dynamic Vacation Calculation per Employee
- **User-Specific Working Hours**: System now checks each employee's individual `dailyWorkingHours` before vacation deductions
- **Proportional Vacation Days**: Vacation days calculated as ratio of actual working hours to standard 8-hour day
- **Smart Day Detection**: Automatically detects non-working days (0 vacation deduction) vs partial days (proportional deduction)
- **Example Logic**: Kevin Saturday 4h = 0.5 vacation days, Kevin Sunday 0h = 0 vacation days, Kevin weekdays 8h = 1.0 vacation days
- **Backend Validation**: Server validates working days per user before processing vacation requests
- **Data Integrity**: Corrected existing records to reflect proper vacation calculations and working hours

## Previous Changes - ATTENDANCE FIXES COMPLETE (August 1, 2025)

### Employee Settings & Statistics Enhancement
- **Employee Statistics Dashboard**: New comprehensive statistics section with vacation balance, overtime totals, and current work hours
- **Vacation History Tracking**: Added "Ultime scalate" section showing last 3 vacation deductions with dates and days used
- **Enhanced Work Schedule Display**: Completely redesigned daily schedule interface with gradients, icons, and color-coded categories
- **Modern Card Design**: Professional cards with hover effects, proper spacing, and visual hierarchy
- **Overtime Statistics**: Real-time calculation of total overtime hours, monthly breakdown, and weekend work tracking
- **Improved Vacation Balance**: Dynamic calculation based on actual vacation records with proper deduction tracking
- **Visual Improvements**: Removed non-paid break display, enhanced UI with modern gradients and better responsive design

### Critical Bug Fixes - Manual Attendance System
- **NaN Hours Bug Fixed**: Backend now prioritizes frontend calculations over timestamp parsing to prevent invalid hours
- **Mixed Day Vacation Logic**: Partial vacation days calculated correctly (4/8 hours = 0.5 days) for mixed work+vacation days
- **Responsive Modal Layout**: Mixed day modal now properly scrollable with responsive grid layout and accessible buttons
- **Calculation Priority**: Frontend hour calculations take precedence over backend timestamp calculations for accuracy

### Task Management System Completed
- **Task Creation & Assignment**: SuperAdmin can create tasks with flexible assignment (specific users or unassigned for self-assignment)
- **Self-Assignment System**: Employees can view and claim unassigned tasks from "Task Disponibili" section
- **Task Completion**: Streamlined completion workflow with green "🎯 COMPLETA TASK" button positioned between Annulla/Aggiorna buttons
- **Task Display**: Cards show assigned user names (simplified format like "KP") and due dates with Italian formatting
- **Default Filtering**: Tasks page opens with "In attesa" filter instead of showing all tasks
- **Comments System**: Full commenting functionality on tasks with real-time updates
- **Permission Handling**: Smart fallback for user display when access is restricted (403 errors)
- **UI Polish**: Single X button on modals, clean layout with proper spacing

### Key Features Implemented
- **Unassigned Task Logic**: Backend properly handles null assignments and "unassigned" values
- **Role-Based Permissions**: Employees can only modify their assigned tasks, admins have full access
- **Visual Indicators**: Priority icons (⚡ ⚠️ ↑ -), completion status with green checkmarks and strikethrough
- **Italian Localization**: Date formats, button labels, and messaging all in Italian
- **Real-time Updates**: Task status changes reflect immediately across the interface

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **React 18** with TypeScript for type safety and modern development patterns
- **ShadCN UI components** built on Radix UI primitives for consistent, accessible interface design
- **TailwindCSS** for utility-first styling with CSS custom properties for theming
- **Wouter** for lightweight client-side routing
- **TanStack Query** for server state management, caching, and synchronization
- **React Hook Form** with Zod validation for robust form handling
- **Vite** as the build tool for fast development and optimized production builds

### Backend Architecture
- **Express.js** server with TypeScript for API endpoints and middleware
- **Session-based authentication** using express-session with secure cookie configuration
- **Role-based authorization** middleware supporting SuperAdmin, Admin, and Employee roles
- **RESTful API design** with consistent error handling and request/response patterns
- **Audit logging** system for tracking all sensitive operations and security events

### Data Storage Solutions
- **File-based JSON storage** as primary database using JSONStorage class
- **Local JSON files** in `/data` directory for all persistent data (users, tasks, attendance, notifications)
- **No external database dependencies** - fully offline capable system
- **Session storage** using in-memory store for development sessions

### Authentication and Authorization
- **Multi-tier role system** with distinct permissions for SuperAdmin, Admin, and Employee roles
- **Bcrypt password hashing** for secure credential storage
- **Session-based authentication** with configurable timeouts and security headers
- **IP address and user agent tracking** for comprehensive audit trails
- **Permission-based UI rendering** to show/hide features based on user roles

### External Dependencies
- **Neon Database** (@neondatabase/serverless) for PostgreSQL cloud hosting
- **Drizzle ORM** for database schema management and type-safe queries
- **ShadCN/UI** component library for consistent design system
- **Radix UI** primitives for accessible component foundations
- **TailwindCSS** for utility-first styling approach
- **Date-fns** for date manipulation and formatting with Italian locale support
- **Zod** for runtime type validation and schema definitions

### Core Features Architecture
- **Task Management**: Hierarchical task system with priorities, assignments, comments, and status tracking
- **Attendance System**: Clock in/out functionality with break tracking and monthly reporting
- **Notification System**: Real-time notifications with read/unread states and push notification support
- **Yellow Card System**: Warning system for task completion failures with escalation tracking
- **Audit Logging**: Comprehensive activity tracking for security and compliance

### Development Environment
- **Replit-optimized** with custom Vite plugins for development experience
- **Hot module replacement** for fast development iteration
- **TypeScript** throughout the stack for type safety and developer experience
- **Path aliases** configured for clean import statements and better code organization