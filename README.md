# Watch Party App

A real-time YouTube watch party application that allows multiple users to join a room and watch videos in sync using WebSockets.

**Live Demo:** [text](https://youtube-watch-party-frontend.onrender.com/)

---

## Features

- Create and join rooms (Creater becomes the host)
- Real-time video synchronization (play, pause, seek)
- Host and Moderator roles
- Remove participants
- Live participants list
- Server-authoritative video timing
- Zustand-based state management

---

## Tech Stack

### Frontend
- React
- Zustand
- Socket.IO Client
- YouTube IFrame API
- Vite

### Backend
- Node.js
- Express
- Socket.IO

---

## Architecture Overview

The backend acts as the **source of truth** for each room.

Each room maintains:

- `Host`
- `Connected sockets`
- `videoId`
- `isPlaying`
- `currentTime`
- `lastUpdate`
- `participants` (Map of `socketId → user`)

### WebSocket Flow

1. Room
    - User creates a room -> a web socket connection is established as role of host
    - User joins via room Id -> a web connection is established as participant
2. Server validates and joins the socket to a room using roomID.
3. When a HOST performs an action (play, pause, seek):
   - Server updates room state.
   - Server broadcasts the event to all participants.
4. When a new user joins:
   - Server sends current room state.
   - Client calculates the correct real-time video position.

The server enforces role-based permissions and synchronization consistency.

---

## Local Setup

### Clone the Repository

```bash
git clone <REPO_URL>
cd <PROJECT_FOLDER>