# Speed Arena Multiplayer Game

Speed Arena is a multiplayer racing game prototype with a Java Spring Boot backend and a React + Vite frontend.

The project is structured into:
- `backend/` — Spring Boot API, security, room management, leaderboard, and real-time racing state.
- `frontend/` — React client, Lobby, Race UI, Leaderboard, and WebSocket multiplayer logic.
- `unity-build/` and `unity-editor/` — Unity assets and build artifacts used for the game.

## What this project does

- Supports user authentication with JWT (`/api/register`, `/api/login`).
- Manages multiplayer race rooms with room creation, joining, and listing.
- Tracks game results in a leaderboard via REST endpoints.
- Uses WebSocket + STOMP for real-time car movement, room sync, map selection, and race start.
- Runs a modern React app with Vite for the frontend experience.

## Architecture overview

### Backend
- Spring Boot 3.3.2 with Java 17
- Spring Web, Spring Data JPA, Spring Security, WebSocket, MySQL Connector
- JWT-based authentication using `app.jwt.secret` and `app.jwt.expiration-ms`
- REST controllers:
  - `AuthController` — `/api/register`, `/api/login`
  - `RoomController` — `/api/rooms/create`, `/api/rooms/join/{roomCode}`, `/api/rooms/{roomCode}`, `/api/rooms/list`
  - `LB_GameResultController` — `/api/results/save`, `/api/results/leaderboard`
  - `TestController` — secure JWT test endpoint `/api/secure-test`
- Real-time WebSocket controller:
  - `/ws-racing` socket endpoint
  - STOMP send destinations: `/app/car.move`, `/app/player.join`, `/app/room.map.select`, `/app/game.start`, `/app/game.ping`
  - Broadcast topics: `/topic/game-state`, `/topic/room/{roomId}`, `/topic/room/{roomId}/players`, `/topic/room/{roomId}/slots`, `/topic/room/{roomId}/map`, `/topic/room/{roomId}/start`, `/topic/room/{roomId}/winner`, `/topic/pong`
- In-memory game room management for demo multiplayer state

### Frontend
- React with Vite
- Routes:
  - `/loading`
  - `/homepage`
  - `/home`
  - `/lobby`
  - `/race`
  - `/leaderboard`
  - `/ws-test`
  - `/game`
- Uses `@stomp/stompjs` and `sockjs-client` for WebSocket connectivity.
- Uses local session storage to keep player identity, selected car color, room code, map selection, and start slot.
- Includes utilities for track generation and multiplayer lobby logic.

## Local setup

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
   - Create or update `backend/src/main/resources/application.properties`.
   - Required local settings typically include:
     - `spring.datasource.url`
     - `spring.datasource.username`
     - `spring.datasource.password`
     - `spring.jpa.hibernate.ddl-auto`
     - `app.jwt.secret`
     - `app.jwt.expiration-ms`
   - This file is intentionally ignored by Git to keep local secrets and database settings private.

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
- Preview frontend build: `npm run preview`
- Run frontend tests: `npm run test:track`
- Run backend: `mvn spring-boot:run`

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
