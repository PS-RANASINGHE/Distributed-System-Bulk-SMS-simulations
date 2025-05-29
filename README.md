# Distributed-Systems-Bulk-SMS-simulations

## 🙋‍♂️ Contributor Role: Pamodh Seshan Ranasinghe

Contributed to the [DS Bulksms Simulation](https://github.com/BishwasWagle/dsproject) project.


## 💬 DS Bulksms Simulation

A distributed system built to simulate the process of sending bulk SMS messages, such as broadcasting messages to students at the University of Oulu. Each SMS costs 0.1 credits from a shared balance. The project showcases effective coordination among microservices handling messaging, billing, and status updates.

---

### 🧱 Architecture Overview

The system is decomposed into microservices for scalability and performance, with each node having its own database and server:

| Node     | Functionality |
|----------|---------------|
| **WebAPI**  | Manages credits (uses `ds` database) |
| **SalesAPI** | Handles bulk SMS campaigns (uses `salesdb`) |
| **RPC Server** | Implements gRPC-based communication between services |

Communication between services is handled through:

- **gRPC** for RPC calls (`get_workspace_credit`)
- **JobQueue** via `arq` workers for background tasks
- **Redis Pub/Sub** for real-time event broadcasting using WebSockets

---

### ⚙️ Technologies Used

| Tool/Tech        | Purpose |
|------------------|---------|
| **Python**       | Core backend language |
| **Starlette**    | ASGI framework for APIs/WebSockets |
| **asyncio**      | Asynchronous task management |
| **PostgreSQL**   | Relational data storage (ds, salesdb) |
| **Redis**        | Pub/Sub and cache layer |
| **Docker**       | Containerization and orchestration |
| **gRPC**         | Microservice communication |
| **WebSocket**    | Real-time data updates |
| **KrispBroadcast** | Custom Redis-based broadcaster |
| **JobQueue (arq)** | Background task processing |
| **Matplotlib**   | Graphical analysis of CPU/Memory usage |

---

### 📊 Performance Evaluation

Tested with:
- `5contacts.csv`
- `5000contacts.csv`

Performance (CPU & memory) was monitored before and during message execution using `system_stats.py`, with results visualized using Matplotlib. Evaluation showed linear scaling of system resource usage with message volume.

---

### 🧪 Usage & Setup

- Docker orchestration for databases and Redis:
  ```bash
  docker-compose -f webapi/docker-compose.yaml up -d
