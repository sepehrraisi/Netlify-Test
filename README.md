# Netlify Test Project

A modern web application built with React, TypeScript, and Netlify, featuring authentication, serverless functions, and forms.

## Features

- 🚀 React 18+ with TypeScript
- 🎨 Tailwind CSS for styling
- 🔒 Authentication with Netlify Identity
- ⚡ Serverless Functions
- 📝 Form handling with Netlify Forms
- 🔄 State management with React Query
- ✅ Testing with Vitest and React Testing Library

## Prerequisites

- Node.js 18+
- npm 8+
- Netlify CLI

## Getting Started

1. Clone the repository
2. Install dependencies:
   ```bash
   npm install
   ```
3. Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```
4. Update environment variables in `.env`

5. Start development server:
   ```bash
   npm run dev
   ```

## Development

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run test` - Run tests
- `npm run preview` - Preview production build locally

## Deployment

The project is automatically deployed to Netlify when changes are pushed to the main branch.

## Project Structure

```
project-root/
├── .github/workflows/    # GitHub Actions workflows
├── functions/           # Netlify Functions
├── src/
│   ├── assets/         # Static assets
│   ├── components/     # React components
│   ├── context/        # React context
│   ├── hooks/          # Custom hooks
│   ├── layouts/        # Layout components
│   ├── pages/          # Page components
│   ├── services/       # API services
│   ├── styles/         # Global styles
│   ├── types/          # TypeScript types
│   └── utils/          # Utility functions
├── public/             # Public assets
└── tests/              # Test files
```

## Contributing

1. Create a feature branch
2. Commit changes
3. Push to the branch
4. Create a Pull Request

## License

MIT
