# Custom GitHub Agents

This directory contains custom GitHub Copilot agents that help maintain the quality and organization of the Awesome-Coolify-Templates repository.

## Available Agents

### 🔍 Template Verifier (`@template-verifier`)
**Purpose:** Validates new template submissions for quality, compliance, and Coolify compatibility.

**Use Cases:**
- Verify new template submissions in pull requests
- Check existing templates for compliance
- Validate docker-compose files against Coolify requirements
- Ensure documentation completeness

**Example Usage:**
```
@template-verifier please verify this template submission
@template-verifier check templates/my-new-template
```

**What It Checks:**
- ✅ Template directory structure
- ✅ Docker Compose validity and Coolify compatibility
- ✅ Environment variable usage and documentation
- ✅ Health check configurations
- ✅ README completeness
- ✅ Security best practices
- ✅ Main README updates

[View Full Documentation](./template-verifier.md)

---

### 📚 Repository Organizer (`@repo-organizer`)
**Purpose:** Maintains repository structure, updates template listings, and ensures consistency.

**Use Cases:**
- Add new templates to main README
- Verify repository organization
- Find orphaned assets
- Generate repository statistics
- Maintain consistency across documentation

**Example Usage:**
```
@repo-organizer add template listing for templates/my-template
@repo-organizer check repository organization
@repo-organizer find orphaned icons and cover pages
```

**What It Does:**
- 📋 Syncs template listings in main README
- 🔗 Validates link integrity
- 📊 Generates repository statistics
- 🎨 Tracks icons and cover pages
- ✨ Ensures consistent formatting

[View Full Documentation](./repo-organizer.md)

---

## How to Use Custom Agents

### In Pull Requests
Mention the agent in a PR comment:
```
@template-verifier please review these changes
```

### In Issues
Ask the agent to perform specific tasks:
```
@repo-organizer generate a repository audit report
```

### During Development
Use agents to verify your work before submitting:
```
@template-verifier check templates/my-new-template
@repo-organizer verify template listing
```

## Agent Workflow

When contributing a new template, use this workflow:

1. **Create Template**
   - Add template files to `templates/your-template/`
   - Write comprehensive README
   - Create valid docker-compose.yaml

2. **Verify Template**
   ```
   @template-verifier check templates/your-template
   ```
   - Fix any issues identified
   - Re-run verification if needed

3. **Update Repository**
   - Add icons/covers to respective directories
   - Update main README with template listing

4. **Organize Repository**
   ```
   @repo-organizer add template listing for templates/your-template
   ```
   - Verify listing is correct
   - Ensure links work

5. **Submit PR**
   - Create pull request with your changes
   - Agents will automatically verify in PR

## Agent Capabilities Summary

| Capability | Template Verifier | Repo Organizer |
|------------|------------------|----------------|
| Validate compose syntax | ✅ | ❌ |
| Check Coolify compatibility | ✅ | ❌ |
| Verify documentation | ✅ | ⚠️ (basic) |
| Update main README | ❌ | ✅ |
| Find orphaned assets | ❌ | ✅ |
| Generate statistics | ❌ | ✅ |
| Security scanning | ✅ | ❌ |
| Link validation | ⚠️ (basic) | ✅ |
| Consistency checks | ⚠️ (template) | ✅ (repository) |

## Testing Agents Locally

You can test agents locally using the Copilot CLI:
```bash
# Install GitHub Copilot CLI
gh copilot --help

# Test an agent
gh copilot agent test template-verifier.md
```

For more information: https://gh.io/customagents/cli

## Contributing to Agents

Found a bug or want to improve agent capabilities?

1. **Report Issues**
   - Open an issue describing the problem
   - Include examples of what the agent missed
   - Suggest improvements

2. **Update Agent Logic**
   - Edit the appropriate `.md` file
   - Update capabilities documentation
   - Test changes locally
   - Submit a PR

3. **Add New Agents**
   - Identify a specific need
   - Create new agent configuration
   - Document usage and capabilities
   - Update this README

## Agent Best Practices

1. **Be Specific** - Give agents clear, specific instructions
2. **Provide Context** - Include template names, file paths, or PR numbers
3. **Review Suggestions** - Agents can make mistakes; review their output
4. **Iterate** - Re-run agents after making fixes
5. **Combine Agents** - Use both agents for comprehensive validation

## Limitations

Agents **cannot**:
- Actually deploy templates to Coolify
- Access external URLs or services
- Make changes directly to your repository
- Test templates in real environments
- Make subjective quality judgments

Agents **can**:
- Analyze code and documentation
- Verify compliance with standards
- Generate reports and suggestions
- Maintain consistency
- Catch common mistakes

## Version Information

- Template Verifier: v1.0.0
- Repository Organizer: v1.0.0
- Last Updated: 2025-12-18

## Resources

- [Custom Agents Documentation](https://gh.io/customagents/config)
- [Copilot CLI Guide](https://gh.io/customagents/cli)
- [Coolify Docker Compose Guide](https://coolify.io/docs/knowledge-base/docker/compose)
- [Repository Contributing Guide](../../CONTRIBUTING.md)

---

**Need Help?** Open an issue or tag the appropriate agent in a discussion!
