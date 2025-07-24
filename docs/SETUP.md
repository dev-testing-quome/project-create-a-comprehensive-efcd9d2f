# Developer Setup Guide - project-create-a-comprehensive

This guide outlines the setup process for developers working on the "create-a-comprehensive" permit management system.  We recommend using Docker for development, but native setup instructions are also provided.

## Prerequisites

* **Required Software Versions:**
    * Python 3.9+
    * Node.js 16+
    * PostgreSQL 14+ (or compatible database)
    * Docker Desktop (for Docker option)
    * Git

* **Development Tools:**
    * Git client
    * Text editor or IDE (VS Code recommended)
    * A web browser (Chrome recommended)
    * Postman or similar API testing tool

* **IDE Recommendations and Configurations:**
    * **VS Code:** Install extensions for Python, JavaScript, Docker, and PostgreSQL. Configure linters (e.g., ESLint for JavaScript, Pylint for Python) and formatters (e.g., Prettier, Black).


## Local Development Setup

### Option 1: Docker Development (Recommended)

1. **Clone Repository:**
   ```bash
   git clone <repository_url>
   cd project-create-a-comprehensive
   ```

2. **Docker Setup Commands:** Ensure Docker and Docker Compose are installed and running.

3. **Development `docker-compose.yml` Configuration:**  (Example - adjust paths as needed)

   ```yaml
   version: "3.9"
   services:
     backend:
       build: ./backend
       ports:
         - "8000:8000"
       environment:
         - DATABASE_URL=postgresql://postgres:password@db:5432/permit_db
         - SECRET_KEY=your_secret_key  # Replace with a strong secret key
         # ... other environment variables ...
       depends_on:
         - db
     frontend:
       build: ./frontend
       ports:
         - "3000:3000"
     db:
       image: postgres:14
       environment:
         - POSTGRES_USER=postgres
         - POSTGRES_PASSWORD=password
         - POSTGRES_DB=permit_db
   ```

4. **Hot Reload Setup:**  The exact setup depends on your frontend framework (e.g., React, Vue, Angular).  Many frameworks offer built-in hot reloading.  For example, if using React with `webpack`, changes will typically be reflected automatically.

5. **Build and Run:**
   ```bash
   docker-compose up -d --build
   ```


### Option 2: Native Development

1. **Backend Setup:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r backend/requirements.txt
   ```

2. **Frontend Setup:**
   ```bash
   cd frontend
   npm install
   ```

3. **Database Setup:**
   * Download and install PostgreSQL.
   * Create a database named `permit_db` with a user `postgres` and password `password` (or your chosen credentials).  Adjust connection details in your `.env` file accordingly.


## Environment Configuration

* **Required Environment Variables:**  (Example - expand as needed)
    * `DATABASE_URL`: PostgreSQL connection string.
    * `SECRET_KEY`:  A strong, randomly generated secret key for security.
    * `PAYMENT_GATEWAY_API_KEY`:  API key for your chosen payment gateway.
    * `EMAIL_HOST`, `EMAIL_PORT`, `EMAIL_USER`, `EMAIL_PASSWORD`: SMTP settings for email notifications.

* **Local Development `.env` File Setup:** Create a `.env` file in the root directory of your project and populate it with your local environment variables:

   ```
   DATABASE_URL=postgresql://postgres:password@localhost:5432/permit_db
   SECRET_KEY=your_secret_key
   # ... other environment variables ...
   ```

* **Configuration for Different Environments:** Use environment variables to manage settings for development, testing, staging, and production environments.  Consider using a configuration management tool (e.g., environment variables, dedicated config files, or a secrets manager).


## Running the Application

1. **Start Commands for Development:**
   * **Docker:** `docker-compose up -d`
   * **Native:**  Start the backend server (e.g., `python manage.py runserver`) and the frontend development server (e.g., `npm start`).

2. **How to Access Frontend and Backend:** The frontend will typically be accessible at `http://localhost:3000` (or the port specified in your `docker-compose.yml` or `package.json`). The backend API will be accessible at `http://localhost:8000` (or its assigned port).

3. **API Documentation Access:** Use a tool like Swagger or generate documentation from your API code.


## Development Workflow

* **Git Workflow and Branching Strategy:** Use Gitflow or a similar branching strategy (e.g., feature branches, pull requests).

* **Code Formatting and Linting Setup:** Configure linters (e.g., ESLint, Pylint) and formatters (e.g., Prettier, Black) in your IDE or using command-line tools.

* **Testing Procedures:** Write unit and integration tests using appropriate frameworks (e.g., pytest for Python, Jest for JavaScript).

* **Debugging Setup:** Use your IDE's debugging tools or command-line debuggers.


## Database Management

* **Running Migrations:** Use database migration tools (e.g., Alembic for Python) to manage schema changes.

* **Seeding Development Data:** Create scripts to populate your database with sample data for testing and development.

* **Database Reset Procedures:**  Implement scripts to easily reset your database to a clean state.


## Testing

* **Running Unit Tests:**  Execute your unit tests using your chosen testing framework (e.g., `pytest` or `npm test`).

* **Running Integration Tests:** Run integration tests to verify interactions between different parts of the system.

* **Test Coverage Reports:** Generate test coverage reports to track your testing progress.


## Common Development Tasks

* **Adding New API Endpoints:**  Follow your API design guidelines and write appropriate tests.

* **Adding New Frontend Components:**  Use your frontend framework's component structure and best practices.

* **Database Schema Changes:** Use database migrations to manage schema changes safely.

* **Adding Dependencies:** Use your package manager (pip, npm) to add new dependencies and update your requirements files.


## Troubleshooting

* **Common Setup Issues:** Check your `.env` file for correct environment variable values. Ensure that all required dependencies are installed and the correct database is running.

* **Port Conflicts Resolution:**  Change the ports used by your application or other running services.

* **Dependency Issues:** Use your package manager's tools to resolve dependency conflicts.

* **Environment Variable Problems:** Double-check your `.env` file and the environment variables used by your application.  Restart your application after making changes to `.env`.


## Contributing

* **Code Style Guidelines:** Adhere to a consistent code style (e.g., PEP 8 for Python, Airbnb style guide for JavaScript).

* **Pull Request Process:** Create pull requests for code changes, including clear descriptions and tests.

* **Issue Reporting:** Report bugs and feature requests using your project's issue tracker.


This guide provides a foundation for development.  Specific details (e.g., exact commands, framework choices) will depend on your project's technology stack.  Remember to consult the documentation for your chosen technologies and frameworks.
