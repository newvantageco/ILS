# Integrated Lens System (ILS)

A comprehensive, enterprise-grade web application for managing integrated lens systems, built with React, TypeScript, Express.js, and PostgreSQL. This system implements a complete 3-portal ecosystem for ECPs, Lab Technicians, and Suppliers.

## 🏗️ Architecture Overview

The ILS follows a **3-Portal Ecosystem** design:

- **ECP Gateway**: Customer-facing portal for order entry, status tracking, and communication
- **Lab Core**: Internal hub for order processing, machine integration, and quality management  
- **Vendor Connect**: Supplier portal for purchase orders, technical documents, and compliance

## ✨ Current Features (Phase 1-2 Complete)

### 🔐 Authentication & Security
- **Multi-role Authentication**: ECPs, Lab Technicians, Engineers, Suppliers, and Admins
- **HIPAA-compliant** security with encrypted data storage
- **Session management** with secure logout and timeout
- **Role-based access control** with granular permissions

### 📋 Order Management
- **Complete order lifecycle** from creation to completion
- **Prescription validation** with real-time error checking
- **Order status tracking** with automated notifications
- **Digital job tray** for lab floor management
- **Order search and filtering** with advanced query capabilities

### 📄 OMA File Processing
- **Upload and parse OMA files** for prescription data
- **Automatic prescription extraction** and validation
- **Trace file management** for complex prescriptions
- **Error handling** for malformed files

### 🛒 Purchase Order System
- **Digital PO creation** with supplier integration
- **Automated PDF generation** for purchase orders
- **Email delivery** of purchase orders to suppliers
- **PO status tracking** and approval workflows

### 💬 Communication System
- **Consult logs** for ECP-Lab communication
- **Real-time messaging** linked to specific orders
- **Message threading** and conversation history
- **Notification system** for urgent communications

### 📚 Document Management
- **Technical document library** for suppliers
- **Spec sheet uploads** and version control
- **Material data management** with batch tracking
- **Document search** and categorization

### 📊 Analytics & Reporting
- **Role-based dashboards** with relevant KPIs
- **Order statistics** and trend analysis
- **Supplier performance metrics**
- **Lab efficiency tracking**

## 🚀 Phase 3 Development (In Progress)

### 🧠 RCA Workbench (Root Cause Analysis)
- **Analytics Dashboard**: Advanced data correlation and analysis
- **Failure Pattern Recognition**: Identify trends in quality issues
- **Machine Performance Analytics**: Track equipment efficiency and errors
- **Material Quality Tracking**: Correlate supplier batches with defects

### 🔧 Digital Calibration & Maintenance
- **Equipment Calibration Schedules**: Automated maintenance tracking
- **SOP Management**: Standard operating procedure documentation
- **Maintenance Logs**: Complete equipment service history
- **Alert System**: Proactive maintenance notifications

### 📈 Enhanced QA System
- **Failure Classification**: Structured defect categorization
- **Photo Documentation**: Visual quality issue tracking
- **Statistical Process Control**: Real-time quality monitoring
- **Non-Conformance Reports**: Automated supplier notifications

### 🔄 Returns & Non-Adapt Management
- **Structured Return Data**: Capture detailed failure information
- **ECP Feedback Integration**: Link returns to original orders
- **Trend Analysis**: Identify recurring adaptation issues
- **Process Improvement**: Data-driven workflow optimization

## 🛠️ Tech Stack

- **Frontend**: React 18, TypeScript, Vite, Tailwind CSS, Radix UI
- **Backend**: Express.js, Node.js, TypeScript
- **Database**: PostgreSQL with Drizzle ORM
- **Authentication**: Passport.js with local and Replit auth
- **Email**: Resend API
- **PDF Generation**: PDFKit
- **State Management**: TanStack Query
- **Charts & Analytics**: Recharts
- **UI Components**: Radix UI primitives

## Getting Started

### Prerequisites

- Node.js 18+ 
- PostgreSQL database
- npm or yarn

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd IntegratedLensSystem
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your configuration
```

4. Set up the database:
```bash
npm run db:push
```

5. Start the development server:
```bash
npm run dev
```

## Environment Variables

Required environment variables:

```env
DATABASE_URL=postgresql://username:password@localhost:5432/database_name
ADMIN_SETUP_KEY=your-secure-admin-setup-key
RESEND_API_KEY=your-resend-api-key
PORT=5000
NODE_ENV=development
```

## Deployment

### Digital Ocean App Platform

1. Connect your GitHub repository to Digital Ocean App Platform
2. Set the following environment variables in the Digital Ocean dashboard:
   - `DATABASE_URL`: Your PostgreSQL connection string
   - `ADMIN_SETUP_KEY`: Secure key for admin account creation
   - `RESEND_API_KEY`: Your Resend API key for email functionality
   - `NODE_ENV`: production

3. Configure build settings:
   - Build Command: `npm run build`
   - Run Command: `npm start`
   - Source Directory: `/`

### Manual Deployment

1. Build the application:
```bash
npm run build
```

2. Start the production server:
```bash
npm start
```

## 📁 Project Structure

```
├── client/                    # React frontend
│   ├── src/
│   │   ├── components/       # Reusable UI components
│   │   │   ├── ui/          # Radix UI component library
│   │   │   ├── examples/    # Component examples
│   │   │   └── *.tsx        # Feature components
│   │   ├── pages/           # Page components (ECP, Lab, Supplier portals)
│   │   ├── hooks/           # Custom React hooks
│   │   └── lib/             # Utility functions and auth
├── server/                   # Express.js backend
│   ├── index.ts             # Main server entry point
│   ├── routes.ts            # API route definitions
│   ├── storage.ts           # Database operations
│   ├── localAuth.ts         # Local authentication
│   ├── replitAuth.ts        # Replit authentication
│   ├── emailService.ts      # Email notifications
│   ├── pdfService.ts        # PDF generation
│   └── vite.ts              # Vite integration
├── shared/                   # Shared types and utilities
│   ├── schema.ts            # Database schema (Drizzle)
│   └── omaParser.ts         # OMA file parsing logic
├── db/                       # Database configuration
│   └── index.ts             # Drizzle database setup
├── dist/                     # Build output
└── attached_assets/          # Project documentation
```

## API Endpoints

### Authentication
- `POST /api/auth/signup-email` - Email/password signup
- `POST /api/auth/login-email` - Email/password login
- `POST /api/auth/logout-local` - Logout
- `GET /api/auth/bootstrap` - Get user info and redirect path

### Orders
- `POST /api/orders` - Create new order
- `GET /api/orders` - List orders (filtered by role)
- `GET /api/orders/:id` - Get order details
- `PATCH /api/orders/:id/status` - Update order status
- `PATCH /api/orders/:id/oma` - Upload OMA file
- `PATCH /api/orders/:id/ship` - Mark order as shipped

### Purchase Orders
- `POST /api/purchase-orders` - Create purchase order
- `GET /api/purchase-orders` - List purchase orders
- `GET /api/purchase-orders/:id/pdf` - Download PDF
- `POST /api/purchase-orders/:id/email` - Email purchase order

### Suppliers
- `GET /api/suppliers` - List suppliers
- `POST /api/suppliers` - Create supplier
- `PATCH /api/suppliers/:id` - Update supplier
- `DELETE /api/suppliers/:id` - Delete supplier

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

MIT License - see LICENSE file for details
