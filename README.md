# Python CI/CD Assignment 2

A minimal Flask application demonstrating a GitHub Actions CI/CD pipeline with Build, Test, and Deploy jobs using Docker.

## Run locally on Windows

1. Install Python 3.12+ and Docker Desktop.
2. Open PowerShell in this project folder.
3. Create and activate a virtual environment:

   ```powershell
   py -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

4. Install dependencies and run tests:

   ```powershell
   python -m pip install -r requirements.txt
   python -m pytest -v
   ```

5. Build and run with Docker:

   ```powershell
   docker build -t python-cicd-app .
   docker run --rm -p 5000:5000 python-cicd-app
   ```

6. Open http://localhost:5000 and http://localhost:5000/health in a browser.

## GitHub Actions

The workflow is at `.github/workflows/ci-cd.yml`. Push to `main` to trigger it. Jobs run in order: Build, Test, Deploy. Deploy starts the container on the GitHub-hosted runner and checks its `/health` endpoint. This is a deployment-stage demonstration, not permanent public hosting.

## What the stages mean

- **Build:** install dependencies and build a Docker image.
- **Test:** run automated tests with pytest. It starts only if Build succeeds.
- **Deploy:** build and start the container, then verify that its health endpoint responds. It starts only if Test succeeds.
