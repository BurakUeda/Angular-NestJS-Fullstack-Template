# Angular and NestJS Fullstack Template

This is a complete, Docker-based fullstack development environment including:
- ⚙️ Angular 19 frontend with TailwindCSS v4
- 🧠 NestJS backend (REST API)
- 🐘 PostgreSQL
- 🌐 Nginx (for serving production builds)

You don't need Node.js installed on your computer — although as a developer, you probably should. 😉

## Requirements
[Docker Desktop](https://www.docker.com/products/docker-desktop) installed and running.

## 🛠️ Installation

### 1) Set Up Database Credentials
Create a `.env` file in the project root:
```dotenv
DB_NAME=app_db
DB_USER=app_user
DB_PASSWORD=supersecurepassword
```
### 2) Create the Angular Frontend
1. Open a terminal in your project’s root folder.
2. Run the following command to generate your Angular app inside the `frontend` folder.
```bash
docker run -it --rm -v "${PWD}/frontend:/app" -w /app node:22 sh -c "npm install -g @angular/cli && ng new YOUR-APP-NAME-HERE --directory=. --style=css --routing --strict --skip-git --skip-install --force"
```
>🔧 Replace  `YOUR-APP-NAME-HERE` with your project name.
3. To enable hot reload (instant updates on file change), edit `frontend/package.json`.
 
Change:
```json
"start": "ng serve",
```
To:
```json
"start": "ng serve --host 0.0.0.0 --port 4200 --poll=1000",
```
### 3) Add TailwindCSS to Angular
1. Inside the `/frontend` folder, run:
```bash
docker-compose exec angular_frontend npm install tailwindcss @tailwindcss/postcss postcss --force
```
2. Create a `frontend/.postcssrc.json` file:
```json
{
  "plugins": {
    "@tailwindcss/postcss": {}
  }
}
```
3. Edit `frontend/src/styles.css` and add:
```css
@import "tailwindcss";
```
### 4) Creating NestJS Backend
1. Open a terminal in your project’s root folder.
2. Run the following command to generate your NestJS app inside the `backend` folder.
```bash
docker run -it --rm -v "${PWD}/backend:/app" -w /app node:22 sh -c "npm install -g @nestjs/cli && nest new app --directory=. --skip-git --package-manager=npm --strict"
```
### 5) Build and Start All Services
Open a terminal in your project’s root folder, and run:
```bash
docker-compose up --build -d
```
>🕐 This may take a minute. Once it's done:
- Open http://localhost:4200 to view the Angular app.
- Use `docker ps` to check that all containers are running.
