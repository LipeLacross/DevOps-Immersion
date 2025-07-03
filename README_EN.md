## 🌐 [Versão em Português do README](README.md)

# DevOps-Immersion

This repository is dedicated to the **Alura & Google Cloud DevOps Immersion**. Learn DevOps in practice with real-world projects, covering essential technologies such as **Docker** (containers), **CI/CD pipelines**, and **Google Cloud Run** for deployment.

Full guide: [alura.tv/guiademergulhodevops](https://alura.tv/guiademergulhodevops)

## 🔨 Project Features

- REST API for school management, enabling:
  - Registering, searching, updating, and deleting **students**
  - **Courses** management
  - Enrolling students in courses
- Containerized deployment with Docker
- Ready for Continuous Integration (CI/CD) and deployment on Google Cloud Run

### 📸 Project Visual Example

<div align="center">
  <img src="https://github.com/user-attachments/assets/584d9aee-57bb-4d24-b948-056467ff4e68" alt="Screenshot 2025-07-03 132707" width="350" style="margin: 8px; border-radius: 8px;">
  <img src="https://github.com/user-attachments/assets/ed764f6c-c4e5-45d0-9efc-b92dce5bd036" alt="Screenshot 2025-07-03 130932" width="350" style="margin: 8px; border-radius: 8px;">
</div>
> The API exposes documented endpoints via Swagger at `/docs` after local or cloud startup.

## ✔️ Techniques and Technologies Used

- **Python** (FastAPI)
- **Docker** & Docker Compose
- **SQLAlchemy** (ORM)
- **SQLite** (local database)
- **Pydantic** (data validation)
- **Google Cloud Run** (deployment)
- **CI/CD** (continuous integration)

## 📁 Project Structure

- **app.py**: FastAPI application initialization and main route inclusion.
- **database.py**: SQLite database configuration and ORM session.
- **models.py**: Table and relationship definitions (Students, Courses, Enrollments).
- **schemas.py**: Pydantic schemas for data validation and serialization.
- **requirements.txt**: Project dependencies.
- **Dockerfile**: Instructions to build the Docker image.
- **docker-compose.yml**: Container orchestration for local environment.
- **escola.db**: SQLite database used by the application.
- **README.md**: Main documentation (this file).
- **README_EN.md**: English version of the documentation.
- **LICENSE**: Project license.

## 🛠️ How to Run the Project Locally

To start the project locally, follow these steps:

1. **Make sure Docker is installed:**
   - Download and install [Docker](https://www.docker.com/).

2. **Clone the Repository:**
   ```
   git clone 
   cd DevOps-Immersion
   ```

3. **Start the application with Docker Compose:**
   ```
   docker-compose up --build
   ```

4. **Access the API:**
   - Go to `http://localhost:8000/docs` to view and test the endpoints via Swagger.

## 🌐 Deploy

To deploy to the cloud using Google Cloud Run, follow these detailed steps:

### 1. Prerequisites

- **Active Google Cloud account**
- **Project** created in Google Cloud
- **Google Cloud SDK** installed on your machine (or use Cloud Shell in the console)
- **Enable required APIs:**
  ```
  gcloud services enable run.googleapis.com
  gcloud services enable cloudbuild.googleapis.com
  ```
- **Authenticate:**
  ```
  gcloud auth login
  ```
- **Set your project:**
  ```
  gcloud config set project YOUR_PROJECT_ID
  ```

**Example of Google Cloud SDK installer screen:**

![Google Cloud SDK Installation Example](https://pplx-res.cloudinary.com/image/private/user_uploads/55317053/d32b6db6-ce42-4950-8426-f30919db9d8e/image.jpg)

> Select:
> - Google Cloud CLI Core Libraries and Tools (required)
> - Bundled Python (recommended)
> - Cloud Tools for PowerShell (optional)
> - Beta Commands (optional)

### 2. Build and Push the Docker Image to Container Registry

In the root directory of the project (where the Dockerfile is), run:

```
gcloud builds submit --tag gcr.io/YOUR_PROJECT_ID/devops-immersion
```
- Replace `YOUR_PROJECT_ID` with your actual Google Cloud project ID.
- This command will build the Docker image and push it to your project's Container Registry.

### 3. Deploy to Cloud Run

Run the following command to create (or update) the service on Cloud Run:

```
gcloud run deploy devops-immersion \
  --image gcr.io/YOUR_PROJECT_ID/devops-immersion \
  --platform managed \
  --region YOUR_REGION \
  --allow-unauthenticated
```
- Replace `YOUR_PROJECT_ID` with your project ID.
- Replace `YOUR_REGION` with the desired region (e.g., `us-central1`, `southamerica-east1`).
- The `--allow-unauthenticated` flag allows public access to the API (remove it if you want restricted access).

During deployment, you may be prompted to confirm the service name and region.

### 4. Access Your Application

After completion, the terminal will display the public URL of your Cloud Run service. Access this URL in your browser to use the API.

**Additional Tips:**

- You can manage your services via the Google Cloud web console in the **Cloud Run** section.
- To configure environment variables, memory, request limits, and other options, consult the official Cloud Run documentation.
- If you want to automate deployment via CI/CD, use a `cloudbuild.yaml` file with build and deploy steps.