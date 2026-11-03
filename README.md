# Solvya Technical Documentation

Technical documentation repository for the **Solvya Healthcare Equipment Management System**.

This repository contains the documentation structure and configuration for maintaining, building, and publishing Solvya technical documentation using MkDocs and Material for MkDocs.

## Documentation status and review boundary

This repository is the documentation site for the Solvya project and is not the source-of-truth implementation repository for the live application. The content in these pages should therefore be treated as a curated design-level documentation package and operational reference for the project, rather than a runtime-verified record of the production application.

When implementation details are described in this site, they should be cross-checked against the authoritative application repository before being used as production truth for deployment, security decisions, or system behavior.

## Technologies Used

- Python
- MkDocs
- Material for MkDocs
- Git and GitHub
- GitHub Actions
- GitHub Pages

## Project Structure

```text
solvya-informational-website/
├── .github/
│   └── workflows/
│       └── deploy.yml
├── docs/
│   ├── assets/
│   │   ├── images/
│   │   └── stylesheets/
│   ├── index.md
│   ├── overview.md
│   ├── architecture.md
│   ├── technical-reference.md
│   ├── api-reference.md
│   ├── database-design.md
│   ├── frontend-documentation.md
│   ├── backend-documentation.md
│   ├── authentication-and-security.md
│   ├── developer-guide.md
│   ├── deployment-guide.md
│   ├── testing.md
│   └── glossary.md
├── mkdocs.yml
├── requirements.txt
├── .gitignore
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.10 or later
- pip
- Git

### Clone the Repository

```bash
git clone git@github.com:akirachix/solvya-informational-website.git
cd solvya-informational-website
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Run Documentation Locally

```bash
mkdocs serve
```

Open http://127.0.0.1:8000/ in your browser.

### Build Documentation

```bash
mkdocs build
```

To check for warnings and errors:

```bash
mkdocs build --strict
```

The generated website is stored in the `site/` directory.

## Deployment

Documentation deployment is configured through GitHub Actions.

Workflow file:

```text
.github/workflows/deploy.yml
```

The workflow builds and deploys the documentation to GitHub Pages when changes are pushed to the `main` branch. Manual execution is also supported.

GitHub Pages must be configured to use GitHub Actions as its deployment source.

## Contributing

- Keep the documentation structure organised.
- Update `mkdocs.yml` when adding new documentation pages.
- Ensure referenced files exist.
- Run `mkdocs build --strict` before submitting changes.