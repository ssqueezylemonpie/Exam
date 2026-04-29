# 📋 IT Exam — Project Planning

## Project Overview

This project involves setting up a Linux-based web server with a MariaDB database backend. The server will host a Flask application, a Jellyfin music server, and a PDF library for books, manga, and light novels. The database will manage users and a ticketing system.

---

## 📁 Folder Structure

```
exam/
├── docs/
│   ├── planning.md        # This file — project planning and roadmap
│   └── readme.md          # User guide and installation instructions
├── server/
│   ├── app.py             # Main Flask application entry point
│   ├── config.py          # Configuration file (DB credentials, paths, etc.)
│   ├── requirements.txt   # Python dependencies
│   ├── routes/
│   │   ├── auth.py        # Login/register routes
│   │   ├── tickets.py     # Ticket management routes
│   │   └── library.py     # PDF library routes
│   ├── templates/         # HTML templates for Flask
│   └── static/            # CSS, JS, and static assets
├── database/
│   └── schema.sql         # SQL schema for MariaDB setup
├── library/
│   └── pdfs/              # Storage for books, manga, and light novels
└── jellyfin/
    └── music/             # Music files served by Jellyfin
```

---

## 🛠️ Technology Stack

| Component        | Technology         |
|------------------|--------------------|
| Operating System | Linux              |
| Web Framework    | Flask (Python)     |
| Database         | MariaDB            |
| Media Server     | Jellyfin           |
| PDF Library      | Flask (custom)     |

---

## 🗄️ Database Design

### Table: `users`
Stores all registered users of the system.

| Column       | Type         | Description                     |
|--------------|--------------|---------------------------------|
| `id`         | INT (PK)     | Unique user ID                  |
| `username`   | VARCHAR(100) | The user's display name         |
| `email`      | VARCHAR(255) | User's email address            |
| `password`   | VARCHAR(255) | Hashed password                 |
| `created_at` | DATETIME     | Timestamp of account creation   |
| `role`       | VARCHAR(50)  | Role (e.g. admin, user)         |

### Table: `tickets`
Stores support or request tickets created by users.

| Column        | Type         | Description                          |
|---------------|--------------|--------------------------------------|
| `id`          | INT (PK)     | Unique ticket ID                     |
| `user_id`     | INT (FK)     | References `users.id`                |
| `title`       | VARCHAR(255) | Short title of the ticket            |
| `description` | TEXT         | Detailed description of the issue    |
| `status`      | VARCHAR(50)  | Status (open, in-progress, closed)   |
| `created_at`  | DATETIME     | When the ticket was submitted        |
| `updated_at`  | DATETIME     | Last time the ticket was updated     |

---

## 📝 Step-by-Step Plan

### Step 1 — Set Up the Linux Environment
- [ ] Update and upgrade the system packages
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```
- [ ] Install required packages: `python3`, `pip`, `mariadb-server`, `git`

---

### Step 2 — Install and Configure MariaDB
- [ ] Install MariaDB
  ```bash
  sudo apt install mariadb-server -y
  sudo mysql_secure_installation
  ```
- [ ] Create a dedicated database and user for the project
  ```sql
  CREATE DATABASE exam_db;
  CREATE USER 'exam_user'@'localhost' IDENTIFIED BY 'yourpassword';
  GRANT ALL PRIVILEGES ON exam_db.* TO 'exam_user'@'localhost';
  FLUSH PRIVILEGES;
  ```
- [ ] Run the schema file to create the `users` and `tickets` tables
  ```bash
  mysql -u exam_user -p exam_db < database/schema.sql
  ```

---

### Step 3 — Set Up the Flask Web Server
- [ ] Install Flask and dependencies
  ```bash
  pip install flask flask-mysqldb python-dotenv
  ```
- [ ] Create the main `app.py` and configure it to connect to MariaDB
- [ ] Set up routes for:
  - User authentication (register, login, logout)
  - Ticket creation and management
  - PDF library browsing

---

### Step 4 — Connect Flask to MariaDB
- [ ] Store database credentials in a `.env` or `config.py` file
  ```
  DB_HOST=localhost
  DB_USER=exam_user
  DB_PASSWORD=yourpassword
  DB_NAME=exam_db
  ```
- [ ] Use `flask-mysqldb` or `PyMySQL` to establish the connection
- [ ] Test that the Flask app can query the `users` and `tickets` tables successfully

---

### Step 5 — Install and Configure Jellyfin (Music Server)
- [ ] Install Jellyfin on Linux
  ```bash
  sudo apt install jellyfin -y
  sudo systemctl enable jellyfin
  sudo systemctl start jellyfin
  ```
- [ ] Configure the media library to point to the `jellyfin/music/` folder
- [ ] Access the Jellyfin dashboard (default: `http://localhost:8096`) and complete initial setup
- [ ] Add music files to the `jellyfin/music/` directory

---

### Step 6 — Set Up the PDF Library
- [ ] Create a Flask route that lists and serves PDF files from the `library/pdfs/` folder
- [ ] Organise PDFs into sub-folders by category:
  ```
  library/pdfs/
  ├── books/
  ├── manga/
  └── light-novels/
  ```
- [ ] Build a simple HTML page in Flask that lets users browse and open PDFs in the browser
- [ ] Optionally, restrict access so only logged-in users can view the library

---

### Step 7 — Write the User Guide (`readme.md`)
- [ ] Document all installation steps clearly
- [ ] Include prerequisites (Linux version, Python version, etc.)
- [ ] Describe how to run the Flask server
- [ ] Explain how to access Jellyfin
- [ ] Explain how to use the ticket system
- [ ] Explain how to browse the PDF library

---

### Step 8 — Testing
- [ ] Test database connection from Flask
- [ ] Test user registration and login
- [ ] Test ticket creation, status updates, and listing
- [ ] Test Jellyfin music playback
- [ ] Test PDF library browsing and file access
- [ ] Check all routes return correct responses

---

### Step 9 — Final Review and Submission
- [ ] Review folder structure matches the plan
- [ ] Ensure `planning.md` and `readme.md` are complete and up to date
- [ ] Clean up any test data from the database
- [ ] Confirm all services (Flask, MariaDB, Jellyfin) start correctly on boot

---

## ✅ Summary Checklist

| Task                                  | Status  |
|---------------------------------------|---------|
| Linux environment ready               | ⬜ Todo |
| MariaDB installed and configured      | ⬜ Todo |
| Database schema created               | ⬜ Todo |
| Flask server set up                   | ⬜ Todo |
| Flask connected to MariaDB            | ⬜ Todo |
| User auth routes working              | ⬜ Todo |
| Ticket system routes working          | ⬜ Todo |
| Jellyfin installed and configured     | ⬜ Todo |
| PDF library set up and accessible     | ⬜ Todo |
| `readme.md` user guide written        | ⬜ Todo |
| Full system tested                    | ⬜ Todo |
