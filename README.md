# ASCII Battle Game (Client-Server)

A networked multiplayer game where players move on a grid, attack adjacent opponents, and compete to be the last one standing. Built with C sockets and pthreads.

---

## Compilation

### Server
```bash
gcc server.c -o server -pthread
```
### Client
```bash
gcc client.c -o client -pthread
```

---

## Quickstart Guide


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

# Gameplay

## Commands

| Command | Format      | Description                               |
|---------|-------------|-------------------------------------------|
| MOVE    | MOVE UP     | Move in direction (UP/DOWN/LEFT/RIGHT)   |
| ATTACK  | ATTACK      | Deals 20 damage to adjacent players        |
| QUIT    | QUIT        | Disconnects from game                     |
| SAY     | SAY \<message\> | Broadcasts \<message\> within the same game instance to all other players    | 

## Rules

* **Grid:** 5x5 with random obstacles (`X`)

* **Movement:**
    * Blocked by obstacles, boundaries, and other players

* **Combat:**
    * Attacks only work on orthogonally adjacent players
    * Players die when HP ≤ 0

* **Winning:** Last player standing wins

# Technical Details

**Protocol:**

* TCP sockets with text-based commands
* State broadcasts after every action
* Thread-safe server with mutex locks

**Error Handling:**

* Invalid moves: "Move blocked: obstacle in the way"
* Invalid attacks: "No targets adjacent to attack"
* Full server: "Server full. Try again later"

```mermaid
flowchart TD
    A[Client] -->|1. Connects| B[Server]
    B -->|2. Assigns Player ID| A
    A -->|3. Sends Commands| B
    B -->|4. Broadcasts State| A
    
    subgraph Command Handling
        A -->|"MOVE <direction>"| B
        A -->|"ATTACK"| B
        A -->|"SAY <message>"| B
        A -->|"QUIT"| B
    end
    
    subgraph Server Processing
        B --> C{Parse Command}
        C -->|MOVE| D[Update Position]
        C -->|ATTACK| E[Check Adjacency\nDeal Damage]
        C -->|SAY| F[Broadcast Message\n"Player X: <text>"]
        C -->|QUIT| G[Remove Player]
        D & E & G --> H[Update Game State]
        H --> I[Broadcast to All]
        F --> I
        I --> J[Send ASCII Grid + Chat]
    end
    
    J -->|Real-time Update| A
    J -->|Real-time Update| K[Other Clients]
    
    style A fill:#cff,stroke:#333
    style B fill:#fcf,stroke:#333
    style F fill:#afa,stroke:#333
```
