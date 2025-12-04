# Advantage One Interactive Portal (AIP)

Advantage One Interactive Portal (AIP) is an advanced, full-featured crime and incident management software designed to streamline and automate various aspects of incident reporting, management, and follow-up. Built as an API-centric solution, AIP leverages a modern technology stack including React, Vite, .NET (with Entity Framework), and MSSQL for robust, scalable, and high-performance functionality across various modules.

## Key Features

### Crime & Incident Management
- Capture, track, and resolve incidents efficiently
- Enhanced user workflows
- Comprehensive incident tracking system

### CRM (Customer Relationship Management)
- Manage client interactions
- Track communication
- Ensure smooth information flow

### CBT (Computer-Based Training)
- Implement training programs for personnel
- Ensure staff are properly equipped to handle incidents

### Additional Features
- Incident Reporting
- Satisfaction Surveys
- Advanced Reporting & Analytics
- Stock Management
- Recruitment Management
- Employee Activity Tracking
- Site Visit Management
- Action Calendar & Task Management

## Technologies Used

### Frontend
- **React** with **TypeScript** - Modern, type-safe UI development
- **Vite** - Fast, modern development and build tooling
- **TailwindCSS** - Utility-first CSS framework
- **Radix UI** - Accessible component primitives
- **Shadcn/ui** - Beautiful, accessible components
- **React Hook Form** with **Zod** - Form validation
- **Redux Toolkit** - State management
- **TanStack Query** - Data fetching and caching
- **Framer Motion** - Animation library
- **Recharts** - Data visualization
- **MSW** - API mocking for development

### Backend
- **.NET** - Robust and scalable API
- **Entity Framework** - ORM for seamless database interaction
- **MSSQL** - Reliable, high-performance relational database
- **CORS** - Configured for secure cross-origin requests

## Getting Started

### Prerequisites
- Node.js 18 or later
- .NET SDK (for backend)
- MSSQL Server (for backend)
- npm or yarn

## 📚 Documentation

**For Production Deployment:**
- 🚀 **[Production Ready Summary](PRODUCTION_READY_SUMMARY.md)** - Start here!
- 📋 [Production Checklist](docs/PRODUCTION_CHECKLIST.md)
- 🔧 [Build Instructions](docs/BUILD_INSTRUCTIONS.md)
- 🔀 [Hybrid Setup Guide](docs/HYBRID_SETUP_GUIDE.md) - Real backend + mock analytics

**All documentation:** See [`docs/`](docs/) folder

### Installation

1. **Clone the repository:**
```bash
git clone https://github.com/advantageonesecurity/COOP_AIP.git
```

2. **Install Frontend Dependencies:**
```bash
cd AIP_UI
npm install
```

3. **Install Backend Dependencies:**
```bash
cd AIP_Backend
dotnet restore
```

### Configuration

#### Frontend Configuration

1. **Environment Variables:**
   - Copy `.env.example` to `.env`
   - Update environment variables as needed:

```bash
cp .env.example .env
```

Key environment variables:
- `VITE_API_BASE_URL` - Backend API URL (default: http://localhost:5128/api)
- `VITE_APP_ENV` - Environment (development, staging, production)
- `VITE_ENABLE_MSW` - Enable/disable API mocking

2. **MSW (Mock Service Worker):**
   - MSW is automatically enabled in development mode
   - Allows frontend development without backend
   - Seamlessly switches to real API when backend is ready

#### Backend Configuration

1. **Database Setup:**
   - Configure MSSQL connection string in `appsettings.json`
   - Run Entity Framework migrations:
   ```bash
   dotnet ef database update
   ```

2. **CORS Configuration:**
   - CORS is pre-configured for cross-origin requests
   - Update CORS policy in backend if needed for your domain

### Running the Application

#### Development Mode

1. **Start the Frontend:**
```bash
cd AIP_UI
npm run dev
```

The frontend will run on `http://localhost:5173` (or next available port)

2. **Start the Backend (when ready):**
```bash
cd AIP_Backend
dotnet run
```

The backend API will run on `http://localhost:5128` (or configured port)

#### Production Build

1. **Build the Frontend:**
```bash
cd AIP_UI
npm run build
```

This will:
- Type-check with TypeScript
- Build optimized production bundle
- Output to `dist` directory
- Strip console.logs and debug statements
- Generate source maps (if configured)
- Create bundle analysis report

2. **Preview Production Build:**
```bash
npm run preview
```

## Project Structure

### Frontend Structure
```
AIP_UI/
├── src/
│   ├── components/      # Reusable React components
│   ├── pages/          # Main application pages
│   ├── services/       # API service layers
│   ├── types/          # TypeScript type definitions
│   ├── config/         # Configuration files
│   ├── hooks/          # Custom React hooks
│   ├── utils/          # Utility functions
│   ├── store/          # Redux store and slices
│   ├── contexts/       # React contexts
│   └── mocks/          # MSW mock handlers
├── public/             # Static assets
└── dist/              # Production build output
```

### Backend Structure
```
AIP_Backend/
├── Controllers/        # API endpoints
├── Models/            # Entity Framework models
├── Services/          # Business logic
├── Data/              # Database context and migrations
└── DTOs/              # Data transfer objects
```

## Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run lint` - Run ESLint
- `npm run mock-api` - Start JSON Server (legacy)

## Deployment

### Vercel Deployment
The project is configured for Vercel deployment with `vercel.json`.

### Netlify Deployment
Alternative deployment configured with `netlify.toml`.

### Manual Deployment
1. Build the project: `npm run build`
2. Deploy the `dist` folder to your hosting provider
3. Ensure proper routing configuration for SPA

## Environment-Specific Configurations

### Development
- MSW enabled for API mocking
- Full console logging
- React DevTools
- Hot module replacement

### Staging
- Real API endpoints
- Limited logging
- Performance monitoring

### Production
- Minified and optimized bundles
- Console logs stripped (except errors/warnings)
- Performance monitoring
- Error tracking (if configured)

## Security Features

- JWT-based authentication
- Protected routes
- CORS configuration
- Input validation with Zod
- SQL injection prevention (Entity Framework)
- XSS protection

## Performance Optimizations

- Code splitting
- Lazy loading of routes
- Image optimization
- Bundle size optimization
- Efficient re-rendering with React.memo
- Virtualized lists for large datasets
- Debounced search inputs

## Browser Support

- Chrome (latest 2 versions)
- Firefox (latest 2 versions)
- Safari (latest 2 versions)
- Edge (latest 2 versions)

## Contributing

We welcome contributions to improve AIP. Please:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For questions or support:
- Open an issue on GitHub
- Email: dibanga2800@gmail.com

## Acknowledgments

- Built with modern React and TypeScript
- UI components from Radix UI and Shadcn
- Backend powered by .NET and Entity Framework
- Database management with MSSQL

---

**Note:** This is an active development project. Some features may be in progress or subject to change.
