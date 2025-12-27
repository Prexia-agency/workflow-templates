# Workflows Templates

Central repository for reusable GitHub Actions workflows for all agency projects.

## Available Workflows

### Security
- `security-base.yml` - GitGuardian + Snyk scanning

### Quality
- `quality-base.yml` - ESLint + Prettier + TypeScript + SonarCloud

### Testing
- `testing-ui.yml` - Playwright E2E + Lighthouse

### Build
- `build-nextjs.yml` - Next.js build with t3-env validation

### Deployment
- `deploy-vercel-preview.yml` - Preview deployments
- `deploy-vercel-production.yml` - Production deployments

### Maintenance
- `post-deploy-audit.yml` - Post-deployment Lighthouse audit
- `maintenance-scheduled.yml` - Weekly security scans

## Usage in Projects

Create `.github/workflows/pipeline.yml` in your project:
```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  security:
    uses: your-agency/workflows-templates/.github/workflows/security-base.yml@main
    secrets:
      GITGUARDIAN_API_KEY: ${{ secrets.GITGUARDIAN_API_KEY }}
      SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}

  quality:
    needs: security
    uses: your-agency/workflows-templates/.github/workflows/quality-base.yml@main

  # ... more jobs
```

## Required Secrets

Each project needs these secrets configured in GitHub Settings:

- `GITGUARDIAN_API_KEY`
- `SNYK_TOKEN`
- `VERCEL_TOKEN`
- `VERCEL_ORG_ID`
- `VERCEL_PROJECT_ID`
- `SONAR_TOKEN` (optional)
- `SENTRY_AUTH_TOKEN` (optional)

## Versioning

- `@main` - Latest version (auto-updates)
- `@v1.0.0` - Specific version (stable)
- `@commit-sha` - Exact commit (maximum stability)

## Updates

When updating workflows, follow semantic versioning:
- Major: Breaking changes
- Minor: New features
- Patch: Bug fixes