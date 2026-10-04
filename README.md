# Geekstober Multi-User Collaborative Whiteboard

A room-based collaborative whiteboard built with the MERN stack and Socket.IO. Authenticated users
can create or join rooms and work together on the same whiteboard in real time.

This repository is also part of **Geekstober**, our open-source contribution event. A few small
features and improvements have intentionally been left open for contributors — have a look at the
[contribution opportunities](#geekstober-contribution-opportunities) below.

## Features

### Authentication

- Register and log in with email and password
- Passwords are hashed with bcrypt
- JWT authentication, protected routes and protected rooms

### Whiteboard

- Freehand drawing
- Lines, arrows, rectangles and circles
- Text
- Sticky notes
- Eraser
- Select, move and resize objects
- Undo / redo
- Clear board
- Choose stroke colour and width

### Collaboration

- Room-based collaboration with shareable room codes
- Real-time updates using Socket.IO
- Participant presence
- Room chat for connected participants (messages are live and are not retained after disconnect/restart)
- Multiple users working on the same board
- Rooms stay isolated from each other

## Tech Stack

| Part           | Technology                     |
| -------------- | ------------------------------ |
| Frontend       | React, Vite, Tailwind CSS      |
| Backend        | Node.js, Express               |
| Database       | MongoDB, Mongoose              |
| Real-time      | Socket.IO                      |
| Authentication | JWT                            |
| Language       | JavaScript (no TypeScript)     |

## Project Structure

```text
frontend/             React + Vite application
  src/components/     Authentication, UI, and whiteboard components
  src/pages/          Landing, account, dashboard, and room pages
  src/services/       REST and Socket.IO clients
backend/              Express + Socket.IO application
  src/config/         Environment and MongoDB connection
  src/controllers/    Authentication and room request handlers
  src/middleware/     Authentication, validation, and errors
  src/models/         User, room, and board schemas
  src/services/       Token, room, and persisted board operations
  src/sockets/        Collaboration and presence events
```


## Getting Started

You need Node.js 18+ and a running MongoDB instance (local install, Docker, or Atlas).

```bash
git clone <repository-url>
```

### Backend

```bash
cd backend
npm install
cp .env.example .env      # then fill in the values
npm run dev
```

### Frontend

```bash
cd frontend
npm install
cp .env.example .env.local
npm run dev
```

## Geekstober Contribution Opportunities

These are suggested, non-critical contribution opportunities. Check the issue tracker before
starting work so maintainers can confirm scope and avoid duplicate effort. Core persistence,
authentication, and room synchronization are maintained application functionality and are not
deliberately broken for contributors.

### Issue #1 — Improve Empty Board UI

**Tag:** `easy`
**Area:** Frontend / UI

**Description:**
When a user opens a room with nothing on it, the board just says a single line of text. It works,
but it does not help new users understand what they can do next.

**What can be done:**
- Improve the empty-board message
- Add a small visual or icon
- Mention the first few tools they can use
- Improve spacing and alignment
- Make the empty state disappear once the user starts drawing

**Where to look:**
`frontend/src/utils/canvas.js` (look for `drawEmptyBoardHint`) and the whiteboard components in
`frontend/src/components/whiteboard/`

**Expected result:**
The empty board feels more welcoming and easier to understand. No drawing behaviour changes.

---

### Issue #2 — Improve Whiteboard Toolbar

**Tag:** `easy`
**Area:** Frontend / UI

**Description:**
All the tools work, but the toolbar can be clearer and nicer to use.

**What can be done:**
- Improve spacing between tools
- Make the active tool more obvious
- Add or improve tooltips
- Improve hover and focus states
- Group related tools together
- Make it work better on smaller screens
- Make disabled states (like Undo with no history) clearer

**Where to look:**
`frontend/src/components/whiteboard/Toolbar.jsx` and `frontend/src/constants/tools.js`

**Expected result:**
Users understand what the tools do without changing how any tool behaves.

---

### Issue #3 — Improve Room Cards and Dashboard

**Tag:** `easy`
**Area:** Frontend / UI

**Description:**
The dashboard lists the user's rooms, but the cards and the empty state can be tidied up.

**What can be done:**
- Improve the room card layout
- Make the room code easier to find and copy
- Improve the copy-code feedback
- Improve the empty-dashboard message
- Show more clearly which rooms you own and which you joined
- Improve the layout on smaller screens

**Where to look:**
`frontend/src/pages/DashboardPage.jsx`

**Expected result:**
The dashboard feels cleaner and easier to scan. Reuse the existing room data — do not change the
rooms API.

---

### Issue #4 — Add Board Metadata to Dashboard

**Tag:** `easy`
**Area:** Backend / MongoDB

**Description:**
Boards are persisted in MongoDB. The dashboard could surface a useful, optional board detail such
as the last update time to help users find recently active rooms.

**What can be done:**
- Add a last-updated value to room summaries
- Display it on dashboard cards with a clear empty state
- Add focused validation or UI coverage for the new metadata

**Where to look:**
`backend/src/models/Board.js` and `backend/src/services/boardService.js`

Please avoid changing the board element format or real-time synchronization.

**Expected result:**
Users can see useful board recency information without changing collaboration behavior.

---

## API and Real-Time Events

REST routes are mounted under `/api`: `GET /health`, `POST /auth/register`, `POST /auth/login`,
`GET /auth/me`, `GET /rooms`, `POST /rooms`, `GET /rooms/:roomId`, and
`POST /rooms/:roomId/join`. All routes except health, registration, and login require a bearer JWT.

Socket.IO authenticates the handshake with `auth.token`. Clients use `room:join` (payload
`{ roomCode }`, acknowledgement includes room, elements and participants), `room:leave`,
`board:sync`, `board:element:upsert` (`{ element }`), `board:element:delete` (`{ elementId }`), and
`board:clear`, and `chat:send` (`{ text }`, maximum 1000 characters). The server broadcasts board
updates and `chat:message` payloads only to that room, and presence through `presence:list`,
`presence:joined`, and `presence:left`; socket-specific errors use `app:error`. Boards are snapshotted
to MongoDB when changed and restored when a room is joined.



## Contributing

Pick an issue, comment on it so nobody duplicates your work, and send a pull request.

1. Fork the repository and create a branch, e.g. `feature/improve-toolbar` or `fix/dashboard-ui`
2. Make your change, keeping it focused on the issue
3. Test it — `cd frontend && npm run build`, and `cd backend && npm test`
4. Commit with a clear message, e.g. `feat: group toolbar tools`
5. Open a pull request and mention the issue you worked on

Please follow the existing code style, avoid unrelated changes, and remove any code you no longer
need.

More details are in [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)
