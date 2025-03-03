# Documentation Directory

This directory contains key documentation files related to the project's architecture, diagrams, and decision records.

## Structure

```text
docs/
│── diagrams/
│   ├── source/      # Stores the original .drawio files
│   ├── exports/     # Stores PNG (or other format) exports
│── decisions/       # Stores Markdown Architectural Decision Records (MADRs)
```

### **diagrams/**

This directory contains architectural and infrastructure diagrams used in project documentation.

- **`source/`**: Contains the original `.drawio` files, which can be edited using [Draw.io](https://www.drawio.com).
- **`exports/`**: Stores exported diagram files (PNG, SVG, or other formats) generated from the source `.drawio` files. These exports are used in Markdown documentation to provide visual references.

#### **Editing `.drawio` Files Online**

Diagrams can be edited directly in Draw.io using the following URL structure:

```text
https://app.diagrams.net/?repo=GITHUB_USERNAME/REPO_NAME&path=docs/diagrams/source/FILENAME.drawio
```

Replace `GITHUB_USERNAME` and `REPO_NAME` with the appropriate values, and `FILENAME.drawio` with the specific file you want to edit.

Alternatively, you can use the following Markdown link format:

```markdown
[Edit Diagram in Draw.io](https://app.diagrams.net/?repo=GITHUB_USERNAME/REPO_NAME&path=docs/diagrams/source/FILENAME.drawio)
```

#### **Syncing Changes Back to GitHub**

Draw.io allows direct integration with GitHub for version control. To sync your changes:

1. Open the `.drawio` file in Draw.io using the link format above.
2. Edit the diagram as needed.
3. Click **File > Save** to push the changes directly to the repository (if using Draw.io's GitHub integration).
4. If working locally, commit and push changes using Git.

### **decisions/**

This directory contains **Markdown Architectural Decision Records (MADRs)**, following the standard format defined at [MADR](https://adr.github.io/madr/).

- Architectural Decision Records (ADRs) document key architectural decisions, along with the context and rationale behind them.
- Each ADR should be created in a structured Markdown format.
- Example filenames: `0001-choose-database.md`, `0002-use-kubernetes.md`.

## **Updating Diagrams**

Diagrams should be modified in the **`diagrams/source/`** directory. PNG and SVG exports should be generated using:

- **GitHub Actions** (to automate exports on push events). See the **[GitHub Actions Workflow](../.github/workflows/drawio-export.yml)** for details.
- **Git pre-commit hooks** (optionally, for local updates before commits)

## **Contributing to Documentation**

- **Diagrams**: Edit `.drawio` files and commit them. The exports will be updated automatically.
- **Architectural Decision Records (ADRs)**: When making an architectural decision, create a new ADR in `docs/decisions/` following the MADR template.

For any questions, refer to the project's contribution guidelines or reach out to the maintainers.
