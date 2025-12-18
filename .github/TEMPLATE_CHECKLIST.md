# Template Checklist

Use this checklist when creating a new template to ensure completeness.

## Pre-Submission Checklist

### Files & Structure
- [ ] Template directory created: `templates/your-template-name/`
- [ ] `docker-compose.yaml` file created
- [ ] `README.md` file created with complete documentation
- [ ] Icons added to `icons/` (optional but recommended)
- [ ] Cover image added to `cover-pages/` (optional but recommended)

### docker-compose.yaml
- [ ] Valid Docker Compose syntax (v3+)
- [ ] All services have meaningful names
- [ ] Environment variables used for configuration
- [ ] No hardcoded secrets or passwords
- [ ] Health checks included where applicable
- [ ] Volumes defined for persistent data
- [ ] Restart policies configured
- [ ] Comments added for complex sections

### README.md Documentation
- [ ] Title matches template directory name
- [ ] Banner/cover image referenced (if exists)
- [ ] Overview section explains what this deploys
- [ ] Architecture diagram or description included
- [ ] Prerequisites section lists external dependencies
- [ ] Step-by-step deployment instructions
- [ ] All environment variables documented with examples
- [ ] Troubleshooting section with common issues
- [ ] Configuration examples provided
- [ ] Success criteria defined

### Testing
- [ ] Template tested on actual Coolify instance
- [ ] All services start successfully
- [ ] Health checks pass
- [ ] Services can communicate with each other
- [ ] External integrations work (if applicable)
- [ ] Documented environment variables are accurate

### Main README Update
- [ ] Template added to "Available Templates" section
- [ ] Description is clear and concise
- [ ] Complexity level indicated (Basic/Intermediate/Advanced)
- [ ] Links to documentation and compose file work

### Quality
- [ ] No sensitive data in files
- [ ] Markdown formatting is correct
- [ ] Links are valid and working
- [ ] Images load correctly
- [ ] Grammar and spelling checked
- [ ] Template solves a real problem
- [ ] Documentation is clear for beginners

## Complexity Levels

**🟢 Basic**
- Single service or simple stack
- Minimal configuration
- No external dependencies
- Quick deployment (< 5 minutes)

**🟡 Intermediate**
- Multiple related services
- Moderate configuration
- Some external dependencies
- Medium deployment time (5-15 minutes)

**🔴 Advanced**
- Complex multi-stack deployment
- Extensive configuration
- Multiple external dependencies
- Longer deployment time (15+ minutes)
- Requires understanding of multiple technologies

## After Submission
- [ ] Pull request created with clear description
- [ ] All CI checks pass (if applicable)
- [ ] Respond to review feedback
- [ ] Make requested changes promptly
