# Contributing to Awesome Coolify Templates

Thank you for your interest in contributing! This repository helps the Coolify community by providing well-documented templates for complex deployments.

## What Makes a Good Template?

A good template submission should:
- ✅ Solve a real deployment challenge that lacks official documentation
- ✅ Be tested and working on Coolify
- ✅ Include clear, step-by-step instructions
- ✅ Document all required environment variables
- ✅ Include troubleshooting tips
- ✅ Be production-ready (not just a "hello world")

## Template Structure

Each template must follow this structure:

```
templates/
└── your-template-name/
    ├── docker-compose.yaml   # The compose file
    └── README.md             # Complete documentation
```

### docker-compose.yaml
- Must be valid Docker Compose format (v3+)
- Use environment variables for all configuration
- Include health checks where applicable
- Add comments for complex sections

### README.md
Your documentation should include:

1. **Title and Banner** (optional)
   ```markdown
   # Template Name
   ![Banner](../../cover-pages/template-banner.png)
   ```

2. **Overview**
   - Brief description of what this deploys
   - Why use this template?

3. **Architecture Diagram** (if complex)
   - ASCII art or description of services

4. **Prerequisites**
   - What needs to be set up first
   - External dependencies

5. **Deployment Steps**
   - Step-by-step instructions
   - How to configure in Coolify
   - All environment variables explained

6. **Configuration**
   - Detailed environment variable documentation
   - Example values

7. **Troubleshooting**
   - Common issues and solutions
   - How to debug

8. **Additional Notes** (optional)
   - Scaling considerations
   - Security notes
   - Performance tips

## Adding Icons and Cover Images

1. Add icon to `icons/` directory
   - Format: PNG with transparency
   - Size: 128x128px or 256x256px
   - Name: `template-name-icon.png`

2. Add cover/banner to `cover-pages/` directory
   - Format: PNG or JPG
   - Size: 1200x400px (3:1 ratio recommended)
   - Name: `template-name-banner.png`

3. Reference in your README:
   ```markdown
   ![Icon](../../icons/template-icon.png)
   ![Banner](../../cover-pages/template-banner.png)
   ```

## Submission Process

1. **Fork** this repository
2. **Create** your template in `templates/your-template-name/`
3. **Add** icons/banners if desired
4. **Update** the main README.md to list your template
5. **Test** your template on a Coolify instance
6. **Submit** a pull request

### Pull Request Checklist

- [ ] Template follows the directory structure
- [ ] README.md is complete with all required sections
- [ ] docker-compose.yaml is tested and working
- [ ] Main README.md updated with template listing
- [ ] Icons/banners added (if applicable)
- [ ] No sensitive data (passwords, keys) in files

## Template Listing in Main README

Add your template to the main README.md under "Available Templates":

```markdown
### [Your Template Name](./templates/your-template-name/)
Brief one-line description of what this deploys.

- **Complexity**: Basic | Intermediate | Advanced
- **Services**: List main services
- **Prerequisites**: Any external dependencies
- **[📖 Documentation](./templates/your-template-name/README.md)** | **[📦 Compose File](./templates/your-template-name/docker-compose.yaml)**
```

## Questions?

Feel free to open an issue for:
- Questions about contributing
- Template ideas and suggestions
- Help with your submission

## Code of Conduct

- Be respectful and constructive
- Help others in the community
- Test before submitting
- Document thoroughly

Thank you for contributing! 🎉
