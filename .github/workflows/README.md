# GitHub Workflows (IA generated)

This directory contains GitHub Actions workflows for the 4D Progress project.

## Workflows

### 1. Create Release Tag (`create-release-tag.yml`)

**Purpose**: Creates and manages release tags for the project.

**Trigger**: Manual dispatch (workflow_dispatch)

**Key Features**:
- Creates tags with a smart versioning system
- Supports custom branch selection
- Uses configurable tag prefixes (default: "21" for main branch)
- Automatically increments version numbers (e.g., `21.1`, `21.2`, etc.)
- Avoids creating duplicate tags on the same commit
- Provides detailed summary output

**Usage**:
1. Go to the "Actions" tab in your repository
2. Select "Create Release Tag" workflow
3. Click "Run workflow"
4. Optionally specify:
   - Branch to tag (defaults to current branch)
   - Tag prefix for main branch (defaults to "21")

**Tag Format**:
- Main branch: `{prefix}.{number}` (e.g., `21.1`, `21.2`)
- Other branches: `{branch-name}.{number}` (e.g., `feature.1`, `dev.3`)

**Permissions Required**:
- `contents: write` - To create and push tags
- `actions: read` - To read workflow context

### 2. Release (`release.yml`)

**Purpose**: Automatically builds and creates GitHub releases when tags are pushed.

**Trigger**: Push to any tag

**Key Features**:
- Runs on macOS for 4D component building
- Resolves dependencies automatically
- Builds the component using 4DBuilder
- Archives and signs the component
- Creates a GitHub release with the built artifact

**Workflow Steps**:
1. **Checkout**: Fetches the repository with full history
2. **Tag Info**: Extracts tag name and commit information
3. **Build Environment**: Sets up macOS build environment (TODO: implementation needed)
4. **Dependencies**: Resolves project dependencies (TODO: implementation needed)
5. **Build**: Compiles the component using 4DBuilder (TODO: implementation needed)
6. **Archive**: Creates and signs a ZIP archive
7. **Release**: Creates a GitHub release with the archive

**Build Environment Requirements**:
- macOS runner (for 4D component building)
- 4DBuilder tool (setup required)
- tool4D utility (setup required)
- packageManager for dependencies (setup required)

**Permissions Required**:
- `contents: write` - To create releases and upload assets
- `actions: read` - To read workflow context

## Typical Workflow

1. **Development**: Work on your branch
2. **Tag Creation**: Use "Create Release Tag" workflow to create a tag
3. **Automatic Release**: The "Release" workflow triggers automatically and builds/releases the component

## Configuration

### Secrets Required
- `PAT_TOKEN`: Personal Access Token for tag operations
- `GITHUB_TOKEN`: Automatically provided by GitHub for releases

### Environment Variables
- Tag prefixes can be customized via workflow inputs
- Archive names are automatically derived from repository name

## Notes

- The Release workflow currently contains TODO items for 4D-specific build setup
- Both workflows are designed to work together for a complete CI/CD pipeline
- The tag creation workflow prevents duplicate tags on the same commit
- Archives are automatically named after the repository
