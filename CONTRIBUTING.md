# Contributing to Actions Job Context Testing

Thank you for your interest in contributing to this repository! This project aims to provide clear, practical examples of GitHub Actions job context usage.

## How to Contribute

### Adding New Workflow Examples

1. Create a new workflow file in `.github/workflows/` with a descriptive name
2. Follow the naming convention: `job-context-[topic].yml`
3. Include clear comments explaining what the workflow demonstrates
4. Use `workflow_dispatch` trigger so the workflow can be tested manually
5. Include comprehensive `echo` statements to display context values

### Workflow Structure Guidelines

Each workflow should:
- Have a clear, descriptive name
- Include triggers: `push`, `pull_request`, and `workflow_dispatch`
- Demonstrate one specific aspect of job context
- Include comments explaining non-obvious behavior
- Use meaningful job and step names

### Example Workflow Template

```yaml
name: Job Context - [Your Topic]

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  workflow_dispatch:

jobs:
  example-job:
    runs-on: ubuntu-latest
    steps:
      - name: Display context
        run: |
          echo "Demonstrating: [what you're showing]"
          echo "Job Status: ${{ job.status }}"
```

### Updating Documentation

When adding a new workflow:
1. Add a section in `README.md` describing the workflow
2. Include key features and concepts demonstrated
3. Provide a brief code example
4. Update the table of contents if needed

### Testing Your Changes

Before submitting:
1. Validate YAML syntax: `yamllint .github/workflows/your-file.yml`
2. Test the workflow by pushing to a branch and triggering it
3. Verify all context values are displayed correctly
4. Check that the workflow completes successfully

### Pull Request Process

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/my-example`)
3. Make your changes
4. Commit with clear, descriptive messages
5. Push to your fork
6. Create a Pull Request with:
   - Clear description of what you're adding
   - Why it's useful
   - Screenshots of workflow runs (if applicable)

## Code Style

- Use 2 spaces for indentation in YAML files
- Keep lines under 100 characters when possible
- Use meaningful variable and step names
- Add comments for complex logic

## Questions?

If you have questions or need clarification, please open an issue.

Thank you for contributing!
