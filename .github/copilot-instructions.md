# 🧑‍💻 Copilot Instructions for DevEx-Docs-Validator

## Project Overview
- **Purpose:** Production-ready template for Developer Experience (DevEx) tools, with a working Jekyll Docs Validator (API & CLI) for documentation quality automation.
- **Main Components:**
  - `/src/`: Python source code (API & CLI, FastAPI-based)
  - `/docs/`: Jekyll documentation site (Markdown, layouts, assets)
  - `Dockerfile`, `devex-deployment.yaml`, `devex-service.yaml`: Containerization & deployment configs
  - `/vendor/`: Bundled Ruby gems for Jekyll

## Architecture & Data Flow
- **API:** FastAPI app in `/src/api.py` exposes endpoints for documentation validation.
- **CLI:** `/src/cli.py` provides command-line access to validation routines.
- **Docs:** `/docs/` is a live Jekyll site, validated by the tool suite.
- **Containerization:** Dockerfile builds both Python and Ruby/Jekyll environments; deployment YAMLs target AWS Lightsail.

## Developer Workflows
- **Build & Run Locally:**
  ```bash
  docker-compose up --build
  # Service runs at http://localhost:8000
  ```
- **Edit Logic:** Modify `/src/api.py` and `/src/cli.py` for new validation rules or endpoints.
- **Dependencies:**
  - Python: Update `requirements.txt`
  - Ruby/Jekyll: Update `Gemfile` and `/vendor/bundle` as needed
- **Docs Preview:**
  - Build Jekyll site: `bundle exec jekyll build` (Ruby gems are vendored)
  - Preview: Open `/docs/_site/index.html` in browser

## Patterns & Conventions
- **Validation Logic:** Centralized in Python (`/src/`). Follows FastAPI conventions for endpoints, Pydantic for data models.
- **Docs Structure:** Jekyll layouts in `/docs/_layouts/`, assets in `/docs/assets/`, Markdown in `/docs/`.
- **Containerization:** Multi-language (Python + Ruby) in one Dockerfile. Use `docker-compose` for orchestration.
- **Deployment:** Use provided YAMLs for AWS Lightsail. Image naming conventions should be updated for new projects.

## Integration Points
- **Jekyll ↔ Python:** Python validator can be run against Jekyll docs before deployment.
- **CI/CD:** Integrate with GitHub Actions (see `.github/workflows/` for examples if present).
- **External:** AWS Lightsail for hosting; Ruby gems vendored for reproducible builds.

## Examples
- **Add a new validation rule:** Edit `/src/api.py` and `/src/cli.py`, update tests if present.
- **Update docs theme:** Edit `/docs/_layouts/page.html` and `/docs/assets/css/main.css`.
- **Deploy:** Build container, push to registry, apply `devex-deployment.yaml` on AWS Lightsail.

---

For more, see [README.md](../README.md) and [Jekyll Docs Validator Docs](https://rick-suspends.github.io/DevEx-Docs-Validator/).
