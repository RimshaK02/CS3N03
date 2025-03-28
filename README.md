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
