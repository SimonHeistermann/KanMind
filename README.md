# 🗂️ KanMan

**KanMan** is a modern, user-friendly Kanban tool that helps teams and individuals organize tasks efficiently.
It combines an intuitive board system with role management, task workflows, and secure user authentication via Django REST Framework.

---

## 🚀 Features

- 🧱 **Intuitive Kanban Board** with customizable columns (To Do, In Progress, Review, Done)
- 👥 **User Roles**: Guest, User, Admin with different permissions
- ✅ **Task Management**: Create, edit, and track task status
- 🔄 **Task Assignment** & review flows
- 💬 **Comment System** for task communication
- 🔐 **Secure Backend** using Django REST Framework + Token Authentication
- 📱 **Responsive Frontend** (HTML, CSS, JS)
- 🌐 **CORS-ready** for local development & production deployment

---

## 🧠 Tech Stack

| Bereich | Technologie |
|----------|--------------|
| **Frontend** | HTML, CSS, JavaScript |
| **Backend** | Django 5.2 + Django REST Framework |
| **Auth** | Django-User + Token-Auth |
| **DB** | SQLite (dev) / PostgreSQL (prod möglich) |
| **Env Management** | `.env` / `env-template` |

---

## 📦 Voraussetzungen

- **Python 3.13+**
- **pip** (Python package manager)
- **(Optional)** Virtual Environment (`venv`)
- **Git**
- **Frontend-Live-Server** (z. B. VSCode Live Server Extension)

---

## 🛠️ Setup (Development)

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/bobyang08250772/kanman.git
cd kanman
```

### 2️⃣ Environment Setup
- Erstelle eine Datei namens .env im Projekt-Root, basierend auf der Vorlage env-template.
- 🔐 Tipp: Verwende env-template als Vorlage für .env, aber commite deine .env nie in Git.

### 3️⃣ Create and Activate a Virtual Environment
```bash
python -m venv venv
source venv/bin/activate   # macOS/Linux
venv\Scripts\activate      # Windows
```

### 4️⃣ Install Dependencies
```bash
pip install -r requirements.txt
```

### 5️⃣ Run Migrations
```bash
python manage.py migrate
```

### 6️⃣ Create a Superuser
```bash
python manage.py createsuperuser
```

### 7️⃣ Run the Development Server
```bash
python manage.py runserver
```

--> Open in browser:
➡️ http://127.0.0.1:8000/

### 8️⃣ Create Guest User for Guest Login

Log into the admin page of the project and create a guest user with the following information:

| Field       | Value                |
|-------------|----------------------|
| **Username** | guest@guest.de      |
| **Email**    | guest@guest.de      |
| **Password** | o6B6<c1x|`N2        |
| **First Name** | Guest             |
| **Last Name**  | User              |

---

## 🌐 Hosting / Production Setup

If you plan to host your project (e.g. on Render, Railway, or your own VPS/server):

### 🔧 Update your .env file

DEBUG=False
SECRET_KEY=<your-production-secret>
ALLOWED_HOSTS=kanman.yourdomain.com
DATABASE_URL=postgres://user:pass@host:port/dbname
CORS_ALLOWED_ORIGINS=https://kanman.yourdomain.com
CSRF_TRUSTED_ORIGINS=https://kanman.yourdomain.com

### 📦 Collect static files
```bash
python manage.py collectstatic
```

### ⚙️ Configure Gunicorn + Reverse Proxy (e.g. Nginx)

Set up Gunicorn as your WSGI server and use Nginx to serve static files and handle HTTPS requests.

Example (conceptually):

Gunicorn listens on 127.0.0.1:8000

Nginx listens on port 80/443 and proxies requests to Gunicorn

### 🔒 SSL Certificates

Use Let’s Encrypt (via Certbot) to enable HTTPS.

### 🧰 Debugging Tips

If you get 403 Forbidden errors:

Check your Browser DevTools → Network tab
→ Ensure the request includes the header:

Authorization: Token <YOUR_TOKEN>

--> Guest users don’t need admin rights, but they must be authenticated (valid token present).

Remember:
👉 Django only loads .env values when the server starts, so after editing your .env, restart it:
```bash
python manage.py runserver
```

### 📁 Project Structure
```bash
kanman/
│
├── core/                  # Django core config (settings, urls, wsgi)
├── dashboard_app/         # Kanban boards & tasks API
├── user_auth_app/         # Registration, login, token auth
├── frontend/              # Frontend (HTML, CSS, JS)
├── env-template           # Environment variable template
├── requirements.txt       # Dependencies
└── manage.py
```

### 🧩 License

MIT License © 2025 Simon Heistermann