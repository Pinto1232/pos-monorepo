# POS System Codebase Overview

## Architecture Overview

This is a modern Point of Sale (POS) system built with:
- Frontend: Next.js/React with TypeScript
- Backend: .NET Core
- Authentication: Keycloak
- Database: Entity Framework Core
- State Management: React Context API
- UI Framework: Material-UI (MUI)

## Key Components

### Backend (.NET Core)

1. Controllers:
- AuthController: Handles authentication with Keycloak integration
- PricingPackagesController: Manages pricing packages and customization
- Other controllers for products, users, and sales

2. Models:
- PosDbContext: Entity Framework context managing database entities
- Various models for packages, features, add-ons, and customizations

### Frontend (Next.js/React)

1. Components:
- CustomPackageLayout: Complex component for package customization
- Layout: Main application layout with routing and providers
- Various UI components for dashboard, sales, and product management

2. Context Providers:
- AuthContext: Manages authentication state and Keycloak integration
- PackageSelectionContext: Handles package selection and customization
- Other contexts for UI state management

3. Features:
- Package customization with multi-step wizard
- Dynamic pricing calculations
- Support for multiple currencies
- Enterprise feature management
- Role-based access control

## Authentication Flow

1. Uses Keycloak for authentication:
- SSO support
- Token refresh mechanism
- Secure session management
- Custom login/logout flows

## Key Features

1. Package Management:
- Custom package creation
- Feature selection
- Add-on management
- Usage-based pricing
- Multi-currency support

2. Enterprise Features:
- Multi-location support
- Advanced analytics
- Security suite
- API & Integration options

3. User Interface:
- Responsive design
- Material-UI components
- Step-by-step wizards
- Dynamic pricing calculations

## Development Patterns

1. React Patterns:
- Context API for state management
- Functional components with hooks
- Memo for performance optimization
- Lazy loading for components

2. Backend Patterns:
- Repository pattern
- Dependency injection
- Entity Framework Core
- RESTful API design

## Security Features

1. Authentication:
- Keycloak integration
- Token-based auth
- Refresh token handling
- Secure session management

2. Authorization:
- Role-based access control
- Feature-based permissions
- Enterprise security features

## Extensibility

The system is designed for extensibility with:
- Modular architecture
- Plugin system for features
- Custom integrations support
- API-first approach

This codebase represents a comprehensive POS solution with modern architecture and extensive
features for both small businesses and enterprise customers.