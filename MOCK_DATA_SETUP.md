# Mock Data Setup

## Overview

This application uses **static mock data files**, not MSW (Mock Service Worker). All mock data is imported directly from TypeScript files in the `src/data/` directory.

---

## Mock Data Files

Located in `src/data/`:

```
src/data/
├── customers.ts              - Customer data
├── mockAnalyticsData.ts      - Analytics/dashboard data
├── mockCustomers.ts          - Customer records
├── mockCustomerSatisfaction.ts - Satisfaction metrics
├── mockDailyActivity.ts      - Daily activity reports
├── mockDropdownData.ts       - Dropdown options
├── mockIncidents.ts          - Incident records
├── mockManagers.ts           - Manager data
├── mockOfficers.ts           - Officer data
├── mockRegions.ts            - Region data
├── mockSites.ts              - Site data
├── mockSiteVisits.ts         - Site visit records
├── pipeline.ts               - Pipeline data
└── users.ts                  - User data
```

---

## How It Works

### Development Mode
- Application imports mock data directly from `src/data/` files
- No service worker or HTTP interception
- Fast and simple

### Production Mode
- Application connects to real API at `VITE_API_URL`
- Mock data files are **not** included in production bundle (tree-shaken)
- Services switch to real API endpoints

---

## Transition to Real API

When the real backend is ready:

### 1. Update Services
Your services already handle both scenarios. Example:

```typescript
// In src/services/customerService.ts
export const getCustomers = async () => {
  if (import.meta.env.DEV) {
    // Development: return mock data
    return mockCustomers
  }
  
  // Production: call real API
  const response = await api.get('/customer')
  return response.data
}
```

### 2. Configure API URL
Set the production API URL in Vercel:

```bash
VITE_API_URL=https://api.yourdomain.com
```

### 3. Deploy
Push to main branch - Vercel will build and deploy with real API connection.

---

## Benefits of Static Mock Data

✅ **Simple** - No service worker setup  
✅ **Fast** - Direct imports, no HTTP overhead  
✅ **Type-safe** - TypeScript validates all mock data  
✅ **No build issues** - No external dependencies  
✅ **Easy to update** - Just edit the TypeScript files  
✅ **Tree-shakeable** - Automatically excluded from production  

---

## No MSW Required

**Important:** This project does **NOT** use MSW (Mock Service Worker).

The `src/mocks/` folder can be safely ignored or deleted. It's not used in the application.

---

## Adding New Mock Data

1. Create a new file in `src/data/`:

```typescript
// src/data/mockNewFeature.ts
export const mockNewFeature = [
  {
    id: 1,
    name: 'Feature 1',
    // ... more fields
  }
]
```

2. Import and use in your component:

```typescript
import { mockNewFeature } from '@/data/mockNewFeature'

const MyComponent = () => {
  const data = mockNewFeature
  // Use data...
}
```

3. When ready, replace with real API call:

```typescript
import { api } from '@/config/api'

const MyComponent = () => {
  const [data, setData] = useState([])
  
  useEffect(() => {
    if (import.meta.env.DEV) {
      setData(mockNewFeature)
    } else {
      api.get('/new-feature').then(res => setData(res.data))
    }
  }, [])
}
```

---

## Environment Variables

### Development
```bash
VITE_API_URL=http://localhost:5128/api
VITE_APP_ENV=development
```

### Production
```bash
VITE_API_URL=https://api.yourdomain.com
VITE_APP_ENV=production
VITE_ENABLE_ANALYTICS=true
VITE_ENABLE_ERROR_TRACKING=true
```

**Note:** No `VITE_ENABLE_MSW` variable needed - not using MSW!

---

## File Structure

```
src/
├── data/                    # ← All mock data here
│   ├── mockCustomers.ts
│   ├── mockSites.ts
│   └── ...
├── services/                # Services handle dev/prod switching
│   ├── customerService.ts
│   ├── siteService.ts
│   └── ...
├── components/              # Components use services
└── pages/                   # Pages use services
```

---

## Best Practices

### 1. Keep Mock Data Realistic
```typescript
// Good: Realistic data structure
export const mockCustomers = [
  {
    id: 1,
    name: 'Acme Corp',
    contactEmail: 'contact@acme.com',
    status: 'active'
  }
]

// Avoid: Fake lorem ipsum data
```

### 2. Match API Response Shape
```typescript
// Mock data should match what API returns
export const mockCustomers: Customer[] = [...]  // Same as API
```

### 3. Use TypeScript Types
```typescript
import { Customer } from '@/types/customer'

export const mockCustomers: Customer[] = [...]
```

### 4. Organize by Feature
```
data/
├── customers/
│   ├── mockCustomers.ts
│   ├── mockCustomerSatisfaction.ts
│   └── index.ts
└── sites/
    ├── mockSites.ts
    ├── mockSiteVisits.ts
    └── index.ts
```

---

## Testing

Mock data makes testing easy:

```typescript
import { mockCustomers } from '@/data/mockCustomers'

describe('CustomerList', () => {
  it('renders customers', () => {
    render(<CustomerList customers={mockCustomers} />)
    expect(screen.getByText('Acme Corp')).toBeInTheDocument()
  })
})
```

---

## Summary

- ✅ Using static TypeScript mock data files
- ✅ Located in `src/data/` directory
- ✅ No MSW or service workers
- ✅ Simple, fast, and type-safe
- ✅ Easy transition to real API
- ✅ No production build issues

---

**Status:** ✅ Production Ready  
**Approach:** Static Mock Data (No MSW)  
**Transition:** Services handle dev/prod switching
