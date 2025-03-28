# ASCII Battle Game (Client-Server)

A networked multiplayer game where players move on a grid, attack adjacent opponents, and compete to be the last one standing. Built with C sockets and pthreads.

---

## 🛠 Compilation

### Server
```bash
gcc server.c -o server -pthread
```
### Client
```bash
gcc client.c -o client -pthread
```

---

## 🚀 Quickstart Guide


**1. Start the server (Terminal 1):**

```bash
./server 12345
```

**2. Connect players (Separate terminals):**
```bash
./client 127.0.0.1 12345
```
* Maximum 4 concurrent players
* Players automatically receive symbols (A-D)

---

# 🎮 Gameplay

## 📜 Commands

| Command | Format      | Description                               |
|---------|-------------|-------------------------------------------|
| MOVE    | MOVE UP     | Move in direction (UP/DOWN/LEFT/RIGHT)   |
| ATTACK  | ATTACK      | Deals 20 damage to adjacent players        |
| QUIT    | QUIT        | Disconnects from game                     |

## ⚔️ Rules

* **Grid:** 5x5 with random obstacles (`#`)

* **Movement:**
    * Blocked by obstacles, boundaries, and other players

* **Combat:**
    * Attacks only work on orthogonally adjacent players
    * Players die when HP ≤ 0

* **Winning:** Last player standing wins
