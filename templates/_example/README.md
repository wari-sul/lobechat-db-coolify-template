# Example Template

This is a placeholder showing the structure for a new template.

## Quick Start

To add a new template, copy this directory structure:

```bash
cp -r templates/_example templates/your-template-name
```

Then edit:
1. `docker-compose.yaml` - Add your services
2. `README.md` - Document your template
3. Update main `README.md` to list your template

## Template README Structure

Your template's README.md should include:

### Required Sections
1. **Title** - Clear, descriptive name
2. **Overview** - What does this deploy?
3. **Prerequisites** - What needs to exist first?
4. **Deployment Steps** - Step-by-step guide
5. **Environment Variables** - All required vars
6. **Troubleshooting** - Common issues

### Optional Sections
- Architecture diagram
- Scaling notes
- Security considerations
- Performance tips

## Example docker-compose.yaml

```yaml
services:
  app:
    image: your-app:latest
    restart: unless-stopped
    environment:
      - APP_URL=${APP_URL:?}
      - DATABASE_URL=${DATABASE_URL:?}
    volumes:
      - app-data:/data
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3

volumes:
  app-data:
```

## Checklist

Before submitting:
- [ ] Template tested on Coolify
- [ ] All environment variables documented
- [ ] README follows structure
- [ ] docker-compose.yaml is valid
- [ ] No hardcoded secrets
- [ ] Health checks included
- [ ] Main README updated

## Need Help?

Check the [Contributing Guide](../../CONTRIBUTING.md) or open an issue!
