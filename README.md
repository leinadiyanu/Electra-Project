# 🗳️ Electra - University Electronic Voting System

A secure, role-based backend system for managing university student elections.

## 📌 Overview

This project is designed for campus elections, allowing students to vote securely using their **matriculation number** and **surname**. There is no public registration—**only preloaded student records** can access the system.

Elections are managed by an **electoral committee**, not admins.

### 🧾 Key Rules:
- Each election can have **one or more positions**, and each position can have **multiple candidates**.
- Voters select **only one candidate per position**.
- The **electoral committee member who creates an election** is automatically the **committee head** for that election.
- Only the **head** can release the results.
- Other committee members have limited access and typically help users understand the voting process.

### ⚙️ Committee Capabilities:
- Create and manage elections
- Add/edit/remove candidates for each position
- Set voting start/end times
- Set result release time
- Release results (head only)

### 🛠️ Admin Capabilities:
- Add/edit/delete student users
- Add/remove electoral committee members


## 🧱 Tech Stack

- **Backend**: Node.js (Express)
- **Database**: PostgreSQL (with connection pooling via pg or PgBouncer)
- **Authentication**: JWT (Matriculation/Registration Number + Surname login)
- **Caching**: Redis (for frequently read data, e.g., election details, “has this student voted?” checks)
- **ORM/Query**: Prisma or Sequelize (optional)
- **Validation**: Joi / Zod
- **Deployment**: Render, Railway, AWS, or VPS with load balancer (e.g., Nginx)
- **Scalability Tools:**
Connection pooling to prevent DB overload
Load balancing for multiple backend instances
Rate limiting for API abuse prevention

## 📈 Scalability & Traffic Handling  

University elections often mean **thousands of voters logging in at once**. To handle this safely and efficiently:  

### 🔹 Database Optimization  
- Add indexes on `matric_number`, `election_id`, and `candidate_id`.  
- Use connection pooling (`pg-pool` or external tools like PgBouncer).  

### 🔹 Caching Layer (Redis)  
- Store session tokens, election details, and “already voted” status.  
- Reduces repeated database hits.  

### 🔹 Vote Processing Queue (Optional)  
- API receives a vote → places it in a queue → worker service writes it to DB.  
- Prevents DB overload during peak hours.  

### 🔹 Load Balancing  
- Deploy multiple backend servers.  
- Use Nginx, HAProxy, or cloud load balancer to distribute requests evenly.  

### 🔹 Rate Limiting & Security  
- Apply middleware (`express-rate-limit`) to block abuse/bot requests.  
- Use HTTPS + secure headers for all API traffic.  

### 🔹 Autoscaling (Cloud Deployment)  
- Host on a scalable platform (Render, Railway, AWS, GCP).  
- Configure autoscaling to spin up more backend instances during heavy voting traffic.  

---

### ⚙️ Integration Overview  

- **Node.js + PostgreSQL** → Core backend & relational DB.  
- **Redis** → Quick lookups for session, election data, and vote checks.  
- **Queue System** → Ensures smooth handling of high-volume votes.  
- **Load Balancer** → Distributes traffic across multiple backend servers.  
- **Autoscaling** → Automatically adjusts resources during peak load.  


## 🔐 Core Features

- Student login with matric number and surname
- One vote per user per election
- Time-based access control (start, end, and result release)
- Role-based access: Admin, Electoral Committee, Student
- Enforced vote integrity and privacy

## 📂 Project Structure (MVC-style)
```
e-voting-system/
│── src/
│   ├── auth/             # Login, JWT handling
│   │   ├── auth.controller.js
│   │   ├── auth.routes.js
│   │   └── auth.service.js
│   │
│   ├── elections/        # Election creation & management
│   │   ├── election.controller.js
│   │   ├── election.routes.js
│   │   └── election.service.js
│   │
│   ├── votes/            # Voting process
│   │   ├── vote.controller.js
│   │   ├── vote.routes.js
│   │   └── vote.service.js
│   │
│   ├── results/          # Result release logic
│   │   ├── result.controller.js
│   │   ├── result.routes.js
│   │   └── result.service.js
│   │
│   ├── middleware/       # Auth checks, validation
│   ├── config/           # DB & env configs
│   └── utils/            # Helper functions
│
│── migrations/           # SQL migrations
│── server.js             # Entry point
│── package.json
│── README.md

```

## 🚀 Getting Started

1. Clone the repo  
   `git clone https://github.com/your-username/university-voting-system.git`

2. Install dependencies  
   `npm install`

3. Set up your `.env`  
```
PORT=5000
DB_URL=postgresql://...
JWT_SECRET=your_jwt_secret
```

4. Run the server  
`npm start` or `nodemon`


