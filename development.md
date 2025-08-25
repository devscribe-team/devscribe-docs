---
title: Development Guide
theme: dark
---

# Development Guide

Learn how to set up a development environment for DevScribe and contribute to the project.

## Development Setup

### Prerequisites

- Node.js 18 or higher
- Git
- A code editor (VS Code recommended)

### Local Development

1. **Fork and clone the repository**
   ```bash
   git clone https://github.com/yourusername/devscribe.git
   cd devscribe
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start development server**
   ```bash
   npm run dev
   ```

4. **Open in browser**
   Navigate to [http://localhost:3000](http://localhost:3000)

## Project Structure

```
devscribe/
├── src/
│   ├── app/           # Next.js app directory
│   ├── components/    # React components
│   ├── lib/           # Utility functions
│   └── styles/        # CSS files
├── public/            # Static assets
└── docs/              # Documentation files
```

## Making Changes

### Adding New Pages

1. Create a new `.md` file in `src/app/(pages)/`
2. Add frontmatter with title and optional icon
3. Update `docs.json` to include the new page

### Component Development

Components are located in `src/components/`. Each component should:

- Be properly typed with TypeScript
- Include JSDoc comments
- Follow the existing naming conventions

## Building for Production

```bash
npm run build
npm start
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

{% callout title="Development Tips" %}
- Use TypeScript for all new code
- Follow the existing code style
- Test your changes thoroughly
- Update documentation as needed
{% /callout %} 