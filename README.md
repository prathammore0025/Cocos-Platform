# Build and Deploy Cocos Project

This project demonstrates the use of GitHub Actions for continuous integration and deployment of a Cocos project. The workflow automates the process of building the project and deploying the build artifacts to the main branch.

## Workflow Overview

### Build Job
- **Trigger:** Runs on `push` and `pull_request` events to the `dev` branch.
- **Environment:** Ubuntu Latest

**Steps:**
1. **Checkout code:** Checks out the repository code.
2. **Setup Node.js:** Sets up Node.js environment (version 18).
3. **Install dependencies:** Installs project dependencies using `npm install`.
4. **Build Project (Commented Out):** Build the project using `npm run build`. Uncomment this step if you want to include the build process.

### Deploy Job
- **Trigger:** Runs after the build job.
- **Environment:** Ubuntu Latest

**Steps:**
1. **Checkout main branch:** Checks out the `main` branch.
2. **Checkout dev branch:** Checks out the `dev` branch into a separate directory (`dev`).
3. **Configure Git user:** Configures Git user details.
4. **Forcefully remove and update build folder:**
   - Ensures the current branch is `main`.
   - Removes the existing build directory (if any).
   - Copies the build directory from the `dev` branch to the `main` branch.
   - Forcefully adds the build directory to the Git staging area.
   - Commits and pushes the changes to the `main` branch.

## Usage

### Setup
- Ensure you have a GitHub repository with a `dev` and `main` branch.
- Place the workflow file under the `.github/workflows` directory in your repository.

### Build
- To enable the build step, uncomment the **Build Project** step in the workflow file.

### Deploy
- The deploy job will automatically execute after a successful build, updating the build folder in the `main` branch.

## Notes
- Ensure that the build directory is not ignored by `.gitignore` if you want to commit it.
- If there are no changes to commit, the workflow will skip committing.
