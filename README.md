# miraifluxyy
add project documentation
# MiRAi - AI Automation Agency Website

A modern, fully-featured React application for an AI automation agency with advanced animations, internationalization, and a serverless backend.

## Table of Contents

1. [Features](#features)
2. [Tech Stack](#tech-stack)
3. [Project Structure](#project-structure)
4. [Getting Started](#getting-started)
5. [Components](#components)
6. [Animations & Effects](#animations--effects)
7. [Internationalization](#internationalization)
8. [Database & Backend](#database--backend)
9. [Styling System](#styling-system)
10. [Security Features](#security-features)
11. [Performance Optimizations](#performance-optimizations)
12. [Browser Compatibility](#browser-compatibility)
13. [Deployment](#deployment)
14. [Testing](#testing)
15. [Troubleshooting](#troubleshooting)
16. [State Management](#state-management)
17. [Accessibility](#accessibility)
18. [Analytics & Monitoring](#analytics--monitoring)

## Features

### Core Features
- Responsive design with mobile-first approach
- Dynamic particle network background
- Animated tree logo
- Multi-language support (EN, ES, IT)
- Contact form with Supabase integration
- Cookie consent management
- SEO optimization with meta tags
- Progressive Web App (PWA) ready

### UI Components
- Animated navigation header
- Language switcher
- Mobile menu
- Feature cards with hover effects
- Rotating text animations
- Social media links
- Footer with dynamic year

### Animations
- Particle network background
- Tree logo animation
- Text fade animations
- Card hover effects
- Menu transitions
- Page transitions

## Tech Stack

### Frontend
- React 18.3.1
- TypeScript 5.5.3
- Vite 5.4.2
- Tailwind CSS 3.4.1
- i18next for internationalization
- React Router 6.22.3
- Lucide React for icons
- React Helmet for SEO

### Backend
- Supabase for database and authentication
- Row Level Security (RLS)
- Email validation constraints

### Development Tools
- ESLint 9.9.1
- PostCSS 8.4.35
- Autoprefixer 10.4.18

## Project Structure

```
├── public/
│   ├── locales/           # Translation files
│   │   ├── en/
│   │   ├── es/
│   │   └── it/
├── src/
│   ├── components/        # React components
│   ├── pages/            # Page components
│   ├── lib/              # Utilities and configurations
│   ├── i18n/             # Internationalization setup
│   └── styles/           # Global styles
├── supabase/
│   └── migrations/       # Database migrations
```

## Getting Started

### Prerequisites
- Node.js 18+
- npm 9+
- Supabase account

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/mirai-website.git

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env

# Start development server
npm run dev
```

### Environment Variables
```env
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

## Components

### ParticleNetwork
```typescript
interface Particle {
  x: number;
  y: number;
  vx: number;
  vy: number;
  size: number;
}

// Configuration
const particleCount = 100;
const connectionDistance = 150;
const moveSpeed = 0.15;
```

### HeaderTree
- Canvas-based animated logo
- Dynamic color changes
- Wind effect simulation
- GPU acceleration

### LanguageSwitcher
- Dropdown menu
- Language detection
- Persistent storage
- Smooth transitions

### ContactForm
- Form validation
- Error handling
- Success feedback
- RLS policies
- Rate limiting

## Animations & Effects

### CSS Animations
```css
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes pulse {
  0%, 100% {
    opacity: 0.8;
  }
  50% {
    opacity: 0.4;
  }
}

@keyframes textEnter {
  0% {
    opacity: 0;
    transform: translateY(15px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
```

### Utility Classes
```css
.gpu-accelerate {
  transform: translateZ(0);
  backface-visibility: hidden;
  perspective: 1000px;
}

.animate-fade-in {
  animation: fadeIn 0.5s ease-out forwards;
}
```

### Particle System
- WebGL rendering
- Dynamic connections
- Responsive particle count
- Performance optimization

## Internationalization

### Supported Languages
- English (en)
- Spanish (es)
- Italian (it)

### Translation Structure
```typescript
interface Translation {
  nav: {
    features: string;
    contact: string;
  };
  hero: {
    subtitle: string;
    title: string;
    phrases: {
      clients: string;
      time: string;
      costs: string;
    };
    cta: string;
  };
  // ... more translations
}
```

### Language Detection
```typescript
i18n
  .use(Backend)
  .use(LanguageDetector)
  .use(initReactI18next)
  .init({
    fallbackLng: 'en',
    supportedLngs: ['en', 'es', 'it'],
    detection: {
      order: ['navigator', 'path', 'localStorage'],
    },
  });
```

## Database & Backend

### Tables
```sql
CREATE TABLE contact_submissions (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at timestamptz DEFAULT now(),
  name text NOT NULL,
  email text NOT NULL,
  service text NOT NULL,
  company_name text NOT NULL,
  problems text NOT NULL,
  additional_info text,
  CONSTRAINT valid_email CHECK (email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$')
);
```

### Security Policies
```sql
ALTER TABLE contact_submissions ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Enable insert for all users"
  ON contact_submissions
  FOR INSERT
  TO public
  WITH CHECK (true);

CREATE POLICY "Enable select for authenticated users only"
  ON contact_submissions
  FOR SELECT
  TO authenticated
  USING (true);
```

## Styling System

### Tailwind Configuration
```javascript
module.exports = {
  content: ['./index.html', './src/**/*.{js,ts,jsx,tsx}'],
  theme: {
    extend: {
      fontFamily: {
        mono: ['JetBrains Mono', 'monospace'],
      },
    },
  },
};
```

### Custom Utilities
```css
@layer components {
  .input-base {
    @apply w-full px-4 py-3 bg-black rounded-lg border border-zinc-800;
  }

  .button-base {
    @apply inline-flex items-center justify-center transition-all duration-200;
  }

  .card-base {
    @apply bg-zinc-900/50 backdrop-blur-sm border border-zinc-800 rounded-xl;
  }
}
```

## Security Features

### Form Validation
- Email format validation
- Required field checks
- SQL injection prevention
- XSS protection

### RLS Policies
- Public insert access
- Authenticated read access
- Rate limiting
- Data sanitization

### Cookie Security
- Secure flags
- HttpOnly
- SameSite policy
- Expiration handling

## Performance Optimizations

### Code Splitting
```javascript
const ParticleNetwork = lazy(() => import('./components/ParticleNetwork'));
const ContactForm = lazy(() => import('./pages/ContactForm'));
```

### Bundle Optimization
```javascript
build: {
  rollupOptions: {
    output: {
      manualChunks: {
        'react-vendor': ['react', 'react-dom'],
        'router': ['react-router-dom'],
        'i18n': ['i18next', 'react-i18next'],
      },
    },
  },
  chunkSizeWarningLimit: 1000,
  cssCodeSplit: true,
  minify: 'terser',
}
```

### Image Optimization
- Lazy loading
- WebP format
- Responsive sizes
- CDN delivery

### Font Loading
```html
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link rel="preload" href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&display=swap" as="style" />
```

## Browser Compatibility

### Supported Browsers
- Chrome 100+
- Firefox 100+
- Safari 15+
- Edge 100+
- iOS Safari 15+
- Android Chrome 100+

### Progressive Enhancement
- CSS Grid fallbacks
- Flexbox fallbacks
- Animation fallbacks
- WebGL detection

### Mobile Optimization
- Touch events
- Viewport meta
- Input handling
- Gesture support

## Deployment

### Netlify Configuration
```toml
[build]
  command = "npm run build"
  publish = "dist"

[build.environment]
  NODE_VERSION = "18"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

### Environment Setup
```bash
# Install Netlify CLI
npm install netlify-cli -g

# Login to Netlify
netlify login

# Deploy
netlify deploy --prod
```

## Testing

### Unit Tests
```typescript
import { render, screen, fireEvent } from '@testing-library/react';
import ContactForm from './ContactForm';

test('submits form successfully', async () => {
  render(<ContactForm />);
  
  fireEvent.change(screen.getByLabelText(/name/i), {
    target: { value: 'John Doe' },
  });
  
  // More test implementation...
});
```

### E2E Tests
```typescript
describe('Contact Form', () => {
  it('submits successfully', () => {
    cy.visit('/contact');
    cy.get('input[name="name"]').type('John Doe');
    // More test implementation...
  });
});
```

## State Management

### Custom Hooks
```typescript
const useScrollPosition = () => {
  const [scrollY, setScrollY] = useState(0);
  
  useEffect(() => {
    const handleScroll = () => setScrollY(window.scrollY);
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);
  
  return scrollY;
};
```

### Context Providers
```typescript
const LanguageContext = React.createContext({
  language: 'en',
  setLanguage: (lang: string) => {},
});
```

## Accessibility

### ARIA Labels
```jsx
<button
  aria-label="Toggle menu"
  aria-expanded={isOpen}
  onClick={toggleMenu}
>
```

### Keyboard Navigation
```jsx
<div
  role="menu"
  tabIndex={0}
  onKeyDown={handleKeyDown}
>
```

### Focus Management
```typescript
const handleModalOpen = () => {
  setIsOpen(true);
  modalRef.current?.focus();
};
```

## Analytics & Monitoring

### Performance Monitoring
```typescript
// Web Vitals
reportWebVitals(console.log);

// Custom metrics
performance.mark('componentRender');
```

### Error Tracking
```typescript
window.onerror = (message, source, lineno, colno, error) => {
  // Error handling logic
};
```

### User Analytics
```typescript
const trackPageView = (page: string) => {
  // Analytics implementation
};
```

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT License - see LICENSE.md for details
