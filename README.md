# 📝 Noteverse

**Noteverse** is a full-stack notes management web application that allows users to securely create, edit, and delete their personal notes.  
It provides user authentication, robust error handling, rich text editing, application logging, and automated testing — built for both performance and reliability.

---

## 🚀 Project Overview

The goal of **Noteverse** is to deliver a seamless note-taking experience with complete privacy and maintainability.  
It includes **frontend and backend integration**, **unit testing**, **logging**, and **database connectivity** using **MySQL**.

---

## 🧠 Features

### 🔐 User Authentication & Authorization
- Secure signup, login, and logout.
- User-specific notes — each user can only view and manage their own.
- JWT-based authentication.

### 🗒️ Notes Management
- Create, edit, and delete notes.
- Rich text editor for enhanced note formatting.
- Responsive UI built with React and Vite.

### 🧪 Unit Testing
- **Frontend:** Tested with **Vitest** and React Testing Library.
- **Backend:** Tested with **Vitest** and Supertest for API endpoints.
- Focus on controllers, services, and database logic.

### 📊 Code Quality (SonarQube)
- Integrated **SonarQube** for static code analysis.
- Code quality metrics and linting for cleaner and safer code.

### 🗄️ Database
- **MySQL** used for data persistence.
- Stores users, notes, and related data.
- Designed with relational schema for scalability.

### ⚙️ Version Control (Git)
- Proper branching and merging strategies.
- Organized commits for feature and bug tracking.

---

## 🖥️ Technology Stack

| Layer | Technology |
|:------|:------------|
| **Frontend** | React.js (Vite) |
| **Backend** | Node.js (Express.js) |
| **Database** | MySQL |
| **Testing** | Vitest |
| **Code Quality** | SonarQube |
| **Version Control** | Git & GitHub |

---

## 🧩 Application Structure

### Frontend (React + Vite)
- Interactive dashboard showing user notes.
- Rich text editor for note creation.
- Responsive design for desktop & mobile.
- API integration with Node.js backend.

### Backend (Node.js + Express)
- RESTful API for CRUD operations.
- Authentication middleware using JWT.
- Integrated Pino Logger for structured logs.
- MySQL database interaction via ORM or query builder.

---

## 🧭 Screens Overview

### 🟢 Sign Up / Log In
- **Components:** Sign-up form, Login form  
- **Operations:** Register new user, authenticate existing user, redirect to dashboard.

### 🟡 Dashboard
- **Components:** List of user-specific notes, “Create New Note” button.  
- **Operations:** Fetch user notes, view all, navigate to note editor.

### 🔵 Note Editor
- **Components:** Rich text editor, Save/Cancel buttons.  
- **Operations:** Create or edit notes, save to backend, return to dashboard.

### ⚪ User Profile *(optional)*
- **Components:** User details, Logout button.  
- **Operations:** View profile info, securely log out.

---

## 🧰 Installation & Setup

### Prerequisites
- **Node.js** (LTS recommended) and **npm**
- **MySQL** 8.x (or compatible) running locally or reachable on your network

### 1️⃣ Clone the repository
```bash
git clone https://github.com/Tech-Hammad/NoteVerse.git
cd NoteVerse
```

### 2️⃣ Create the MySQL database
Create an empty database (name it whatever you prefer; the example below uses `noteverse`):

```sql
CREATE DATABASE noteverse CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

The app expects **`users`** and **`notes`** tables. If you do not already have them, run something like the following in your MySQL client (adjust types if your existing schema differs):

```sql
USE noteverse;

CREATE TABLE users (
  userID INT UNSIGNED NOT NULL AUTO_INCREMENT,
  username VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL,
  password VARCHAR(255) NOT NULL,
  isAdmin TINYINT(1) NOT NULL DEFAULT 0,
  profile_image VARCHAR(255) NULL,
  PRIMARY KEY (userID),
  UNIQUE KEY uq_users_email (email)
);

CREATE TABLE notes (
  id INT UNSIGNED NOT NULL AUTO_INCREMENT,
  user_id INT UNSIGNED NOT NULL,
  title VARCHAR(500) NOT NULL,
  note LONGTEXT NOT NULL,
  pinned TINYINT(1) NOT NULL DEFAULT 0,
  secured TINYINT(1) NOT NULL DEFAULT 0,
  password VARCHAR(255) NULL,
  archived TINYINT(1) NOT NULL DEFAULT 0,
  tags JSON NULL,
  PRIMARY KEY (id),
  KEY idx_notes_user_id (user_id),
  CONSTRAINT fk_notes_user FOREIGN KEY (user_id) REFERENCES users (userID) ON DELETE CASCADE
);
```

### 3️⃣ Backend environment variables
In the **`backend`** folder, create a **`.env`** file (never commit real secrets):

```env
PORT=5000
DB_HOST=localhost
DB_USER=root
DB_PASS=your_mysql_password
DB_NAME=noteverse
JWT_SECRET=use_a_long_random_secret_string
```

- **`PORT`**: defaults to `5000` if omitted.
- **`JWT_SECRET`**: required for signing login tokens.

### 4️⃣ Install and run the backend
```bash
cd backend
npm install
npm run dev
```

The API listens on **`http://localhost:5000`** (or your configured `PORT`).

### 5️⃣ Install and run the frontend
Open a **second** terminal:

```bash
cd frontend
npm install
npm run dev
```

The UI is served by Vite at **`http://localhost:5173`**.

**Note:** The frontend calls the API at **`http://localhost:5000`** in several places. Keep the backend on port **5000**, or update those URLs to match your backend.

### 6️⃣ Uploads folder
File uploads are stored under **`backend/uploads/`**. Ensure that directory exists and is writable when you run the backend (it is ignored by Git).

### 7️⃣ Tests (optional)
From the **backend** folder:
```bash
npm test
```

From the **frontend** folder:
```bash
npm test
```

### 8️⃣ Production build (frontend only)
```bash
cd frontend
npm run build
npm run preview
```

`preview` serves the production build locally for a quick check.
