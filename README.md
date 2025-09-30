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

## 🔐 Core Features

- Student login with matric number and surname
- One vote per user per election
- Time-based access control (start, end, and result release)
- Role-based access: Admin, Electoral Committee, Student
- Enforced vote integrity and privacy

## 📂 Project Structure (MVC-style)
```
/src
┣ /controllers
┣ /models
┣ /routes
┣ /middleware
┣ /utils
┗ server.js
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


