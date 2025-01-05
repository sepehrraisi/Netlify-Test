# Product Requirements Document: AI Agent Instructions for Netlify Project Development

## 1. Project Overview

### 1.1 Objective
Create a complete web application that demonstrates modern web development practices and deploys automatically to Netlify's hosting platform.

### 1.2 Core Requirements
- Implement a responsive, modern web interface
- Utilize Netlify's core features including Functions, Forms, and Identity
- Implement continuous deployment
- Follow security best practices
- Ensure cross-browser compatibility

## 2. Technical Requirements

### 2.1 Development Stack
- Frontend Framework: React 18+
- Build Tool: Vite
- CSS Framework: Tailwind CSS
- State Management: React Query + Context API
- Form Handling: React Hook Form
- API Integration: Netlify Functions
- Authentication: Netlify Identity
- Testing: Vitest + React Testing Library

### 2.2 Project Structure
```
project-root/
├── .github/
│   └── workflows/
│       └── main.yml
├── functions/
│   ├── api/
│   └── auth/
├── src/
│   ├── assets/
│   ├── components/
│   ├── context/
│   ├── hooks/
│   ├── layouts/
│   ├── pages/
│   ├── services/
│   ├── styles/
│   ├── types/
│   ├── utils/
│   ├── App.tsx
│   └── main.tsx
├── public/
├── tests/
├── .env.example
├── .gitignore
├── netlify.toml
├── package.json
└── README.md
```

## 3. Feature Implementation Instructions

### 3.1 Initial Setup
1. Create new repository with the specified structure
2. Initialize project with Vite:
```bash
npm create vite@latest my-netlify-project -- --template react-ts
```
3. Configure Tailwind CSS
4. Set up ESLint and Prettier
5. Configure Netlify CLI:
```bash
npm install -g netlify-cli
netlify init
```

### 3.2 Authentication Implementation
1. Enable Netlify Identity
2. Create authentication context
3. Implement login/signup flows
4. Add protected routes
5. Implement password reset functionality

### 3.3 API Integration
1. Create Netlify Functions for:
   - User management
   - Data operations
   - External API integrations
2. Implement error handling
3. Add rate limiting
4. Set up monitoring

### 3.4 Form Handling
1. Set up Netlify Forms
2. Implement form validation
3. Add spam protection
4. Create success/error states
5. Set up form submissions handling

## 4. Netlify Configuration and Deployment

### 4.1 Initial Netlify Setup
1. Create Netlify Account:
   - Visit netlify.com and sign up
   - Connect your GitHub account
   - Enable two-factor authentication

2. Install Netlify CLI:
```bash
npm install netlify-cli -g
netlify login
```

3. Initialize Project:
```bash
netlify init
```

4. Configure Build Settings in Netlify Dashboard:
   - Build command: `npm run build`
   - Publish directory: `dist`
   - Node version: 18.x
   - Enable automatic deployments
   - Configure deploy contexts (production/staging)

### 4.2 Domain Configuration
1. Custom Domain Setup:
   - Add custom domain in Netlify dashboard
   - Configure DNS settings
   - Enable HTTPS
   - Set up redirects from www to non-www (or vice versa)

2. DNS Configuration:
```
A     @     104.198.14.52
CNAME www   yoursitename.netlify.app
```

### 4.3 Netlify Features Setup

1. Netlify Identity:
```javascript
// Install dependencies
npm install netlify-identity-widget

// Initialize in index.html
<script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>

// Initialize in your app
import netlifyIdentity from 'netlify-identity-widget'
netlifyIdentity.init()
```

2. Netlify Forms:
```html
<form name="contact" method="POST" data-netlify="true">
  <input type="hidden" name="form-name" value="contact" />
  <!-- Form fields -->
</form>
```

3. Netlify Functions:
```bash
# Create functions directory
mkdir netlify/functions

# Create example function
touch netlify/functions/hello.js
```

Example function:
```javascript
exports.handler = async function(event, context) {
  return {
    statusCode: 200,
    body: JSON.stringify({ message: "Hello World" })
  }
}
```

### 4.4 netlify.toml Configuration
```toml
[build]
  command = "npm run build"
  publish = "dist"
  functions = "functions"

[dev]
  command = "npm run dev"
  port = 3000
  targetPort = 5173

[[redirects]]
  from = "/api/*"
  to = "/.netlify/functions/:splat"
  status = 200

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"
    Content-Security-Policy = "default-src 'self'"
```

### 4.5 Advanced Configuration

1. Split Testing:
```toml
[split_testing]
  enabled = true

[[split_testing.variants]]
  name = "original"
  percentage = 50

[[split_testing.variants]]
  name = "experiment"
  percentage = 50
```

2. Headers and Security Configuration:
```toml
[[headers]]
  for = "/assets/*"
  [headers.values]
    Cache-Control = "public, max-age=31536000"
```

3. Serverless Functions Configuration:
```toml
[functions]
  directory = "netlify/functions"
  included_files = ["database/**"]
  external_node_modules = ["@aws-sdk/*"]
  node_bundler = "esbuild"
```

4. Edge Functions Configuration:
```toml
[[edge_functions]]
  function = "transform"
  path = "/api/*"
```

### 4.6 Build Plugins
1. Install essential Netlify plugins:
```bash
# Essential plugins
netlify plugin:install @netlify/plugin-lighthouse
netlify plugin:install @netlify/plugin-sitemap
netlify plugin:install netlify-plugin-submit-sitemap
netlify plugin:install netlify-plugin-inline-critical-css
```

2. Plugin configuration in netlify.toml:
```toml
[[plugins]]
  package = "@netlify/plugin-lighthouse"

  [plugins.inputs]
    output_path = "reports/lighthouse.html"

[[plugins]]
  package = "netlify-plugin-inline-critical-css"

[[plugins]]
  package = "@netlify/plugin-sitemap"
  [plugins.inputs]
    buildDir = "dist"
    prettyURLs = true
```

### 4.7 Environment Variables
1. Required variables:
```
VITE_API_URL=
VITE_SITE_URL=
NETLIFY_AUTH_TOKEN=
DATABASE_URL=
```
2. Set up in Netlify dashboard
3. Include local `.env.example`

## 5. Testing Requirements

### 5.1 Test Implementation
1. Unit tests for components
2. Integration tests for API calls
3. E2E tests for critical paths
4. Performance testing
5. Security testing

### 5.2 Test Coverage Requirements
- Minimum 80% code coverage
- Critical paths 100% covered
- All API endpoints tested

## 6. Documentation Requirements

### 6.1 Technical Documentation
1. API documentation
2. Component documentation
3. Setup instructions
4. Deployment guide
5. Testing guide

### 6.2 User Documentation
1. User guides
2. FAQ
3. Troubleshooting guide
4. Security guidelines

## 7. Performance Requirements

### 7.1 Core Web Vitals Targets
- LCP (Largest Contentful Paint): < 2.5s
- FID (First Input Delay): < 100ms
- CLS (Cumulative Layout Shift): < 0.1
- TTI (Time to Interactive): < 3.8s

### 7.2 Optimization Requirements
1. Image optimization
2. Code splitting
3. Lazy loading
4. Caching strategy
5. Asset compression

## 8. Security Implementation

### 8.1 Required Security Measures
1. Authentication & Authorization
2. Data encryption
3. Input validation
4. XSS protection
5. CSRF protection
6. Rate limiting
7. Error handling

### 8.2 Security Headers
1. Configure security headers in netlify.toml
2. Implement CSP
3. Enable HSTS
4. Set up XFO

## 9. Monitoring and Analytics

### 9.1 Required Monitoring
1. Error tracking
2. Performance monitoring
3. User analytics
4. API monitoring
5. Security monitoring

### 9.2 Analytics Implementation
1. Set up Netlify Analytics
2. Configure error tracking
3. Implement custom event tracking
4. Set up monitoring dashboards

## 10. Quality Assurance

### 10.1 Code Quality Requirements
1. Follow ESLint configuration
2. Maintain consistent code style
3. Use TypeScript strictly
4. Document all functions
5. Review pull requests

### 10.2 Testing Requirements
1. Run all tests before deployment
2. Maintain test coverage
3. Update tests with features
4. Document test cases

## 11. Deployment Process

### 11.1 Continuous Deployment
1. Configure GitHub Actions
2. Set up branch protections
3. Implement deployment previews
4. Configure build hooks

### 11.2 Release Process
1. Version control
2. Changelog maintenance
3. Release notes
4. Rollback procedures

## 12. Maintenance Instructions

### 12.1 Regular Maintenance
1. Update dependencies
2. Monitor error logs
3. Review analytics
4. Optimize performance
5. Update documentation

### 12.2 Backup Procedures
1. Database backups
2. Code repository backups
3. Environment configuration backups
4. Documentation backups

## Success Criteria

1. All features implemented and tested
2. Performance metrics met
3. Security requirements satisfied
4. Documentation complete
5. CI/CD pipeline operational
6. Monitoring systems active
7. Production deployment successful

## Delivery Requirements

1. Source code in GitHub repository
2. Complete documentation
3. Test results and coverage reports
4. Performance test results
5. Security audit results
6. Deployment logs
7. Monitoring dashboard access

Remember to maintain clear communication throughout the development process and document any deviations from these requirements with proper justification.