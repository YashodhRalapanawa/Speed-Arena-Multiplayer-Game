# Speed Arena Multiplayer Game

A multiplayer racing game project with a Java Spring Boot backend and a React + Vite frontend.

This repository includes:
- `backend/` — Spring Boot service with REST, security, WebSocket, JPA, and MySQL support.
- `frontend/` — React + Vite app that connects to the backend and renders the game UI.
- `unity-build/` and `unity-editor/` — Unity assets and build output for the game.

## Quick start

1. Clone the project:
   ```bash
   git clone https://github.com/YashodhRalapanawa/Speed-Arena-Multiplayer-Game.git
   cd Speed-Arena-Multiplayer-Game
   ```

2. Install required tools:
   - Java 17
   - Apache Maven
   - Node.js (recommended latest LTS)

3. Configure backend properties:
   - Create or update `backend/src/main/resources/application.properties` with your local database and security settings.
   - This file is intentionally ignored by Git, so each developer keeps their own local config.

4. Run the backend:
   ```bash
   cd backend
   mvn spring-boot:run
   ```

5. Install frontend dependencies and start the app:
   ```bash
   cd ../frontend
   npm install
   npm run dev
   ```

6. Open the frontend URL shown in the terminal (usually `http://localhost:5173`).

## Useful commands

- Start frontend dev server: `npm run dev`
- Build frontend: `npm run build`
- Run frontend preview: `npm run preview`
- Run frontend tests: `npm run test:track`
- Run backend with Maven: `mvn spring-boot:run`

## Notes

- Do not commit `node_modules/`.
- Do not commit local config files such as `application.properties`.
- The root `.gitignore` already ignores:
  - `node_modules/`
  - `**/application.properties`
  - `/target/`
  - `.idea/`
  - `.DS_Store`
  - `unity-build/`

If a file is already tracked by Git and should be ignored, remove it from tracking with:
```bash
git rm --cached path/to/file
```
