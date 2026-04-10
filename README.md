# 🔒 VaultOS — Mini Secure File System

> A browser-based secure file system simulation featuring user authentication, AES-256 encryption, role-based access control, and a full admin dashboard — built as a single self-contained HTML file.

![HTML](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![No Dependencies](https://img.shields.io/badge/dependencies-none-brightgreen?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)

---

## 📸 Preview

```
┌─────────────────────────────────────────────────┐
│  VAULTOS  [ADMIN]  admin     ● AES-256 ACTIVE   │
├──────────┬──────────────────────────────────────┤
│ My Files │  MY FILES                [+ UPLOAD]  │
│ Upload   │  NAME          PERMS   ENC    DATE   │
│ Shared   │  report.pdf    R W D   🔑ENC  2025   │
│ Logs     │  budget.xlsx   R - -   🔑ENC  2025   │
├──────────┤                                      │
│ ADMIN    │                                      │
│ Dashboard│                                      │
│ Users    │                                      │
│ All Files│                                      │
│ Audit Log│                                      │
└──────────┴──────────────────────────────────────┘
```

---

## ✨ Features

### 🔐 Authentication System
- User registration and login with password hashing (SHA-256 simulation)
- Unique session tokens generated on every login
- Failed login attempts are logged with timestamps
- Password change from the settings panel

### 📁 File Storage
- Upload files with name, description, size, and type metadata
- All files flagged as AES-256-GCM encrypted with per-file key display in audit log
- File listing with owner tracking

### 🛡️ Permission System (R / W / D)
- Every file carries independent Read, Write, Delete access control lists
- Share files with specific users by username, or grant public access via `all`
- Permissions enforced on every download and delete operation
- Access violations are logged with severity `WARN`

### 📋 Activity Logging
- Every system event is timestamped and recorded: login, logout, upload, download, delete, permission changes
- Severity levels: `AUTH`, `INFO`, `WARN`, `ERROR`
- Users view their own log; admins see the full system-wide audit trail

### 👑 Admin Dashboard
- Live stats: total users, files stored, log entries, encryption rate
- User management: disable/enable accounts, promote users to admin
- Global file browser across all users
- Full audit log with complete event history

---

## 🚀 Getting Started

No installation required. Just open the file in any modern browser.

```bash
git clone https://github.com/your-username/vaultos.git
cd vaultos
open secure_fs.html        # macOS
# or
start secure_fs.html       # Windows
# or
xdg-open secure_fs.html    # Linux
```

---

## 🧪 Demo Accounts

| Username | Password   | Role  |
|----------|------------|-------|
| `admin`  | `admin123` | Admin |
| `alice`  | `pass123`  | User  |
| `bob`    | `pass456`  | User  |

You can also register new accounts from the login screen.

---

## 🏗️ Project Structure

```
vaultos/
└── secure_fs.html      # Complete application — all HTML, CSS, JS in one file
```

The entire application is self-contained in a single file with no external dependencies, no build step, and no server required.

---

## 🧩 Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    VaultOS Architecture                  │
├─────────────┬──────────────────┬────────────────────────┤
│   AUTH      │   FILE SYSTEM    │      LOGGING           │
│             │                  │                        │
│  Login      │  Upload          │  Per-user activity     │
│  Register   │  Download        │  System audit trail    │
│  Session    │  Delete          │  Severity levels       │
│  Tokens     │  Share           │  Timestamps            │
├─────────────┴──────────────────┴────────────────────────┤
│               IN-MEMORY DATABASE (DB object)             │
│   users[]  ·  files[]  ·  logs[]  ·  sessions           │
├─────────────────────────────────────────────────────────┤
│               ACCESS CONTROL LAYER                       │
│   canRead(file, user)  ·  canWrite()  ·  canDelete()    │
└─────────────────────────────────────────────────────────┘
```

### Key Components

| Component | Description |
|-----------|-------------|
| `DB` object | In-memory state store for users, files, and logs |
| `hash()` | Simple polynomial hash simulating password hashing |
| `canRead/Write/Delete()` | Permission checking functions enforced before every file operation |
| `addLog()` | Centralized logging called on every user action |
| `showView()` | Single-page app router that renders the correct panel |
| Admin views | Gated behind `currentUser.role === 'admin'` checks |

---

## 🔒 Security Concepts Demonstrated

| Concept | Implementation |
|---------|---------------|
| Password Hashing | Polynomial hash (simulates SHA-256 / bcrypt) |
| Session Management | Random 32-char hex token per login |
| Encryption at Rest | AES-256-GCM simulation with per-file key display |
| Role-Based Access Control | `admin` vs `user` roles with different UI and data access |
| Discretionary Access Control | Per-file R/W/D lists set by file owner |
| Audit Logging | Every action logged with user, timestamp, and severity |
| Principle of Least Privilege | Users only see and act on files they have permission for |

> **Note:** This is a frontend simulation for educational purposes. Cryptographic operations are simulated — no real encryption is performed in the browser. For production systems, use a backend with proper crypto libraries (e.g., Node.js `crypto`, Python `cryptography`).

---

## 📚 Learning Objectives

This project is designed for students learning about:

- Authentication flows (login, register, session tokens)
- Access control models (DAC — Discretionary Access Control)
- Security audit logging and event tracking
- Role-based UI rendering (admin vs regular user)
- Secure system design patterns

---

## 🛠️ Extending the Project

Ideas for taking this further:

- **Real encryption** — Use the [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API) (`crypto.subtle`) for actual AES-256-GCM encryption in the browser
- **Persistent storage** — Replace the `DB` object with `localStorage` or `IndexedDB`
- **Backend** — Add a Node.js / Express or Python Flask backend with a real database
- **File content** — Allow reading and editing file content in-browser
- **2FA** — Add TOTP-based two-factor authentication
- **Password strength meter** — Enforce stronger password policies on registration

---

## 📄 License

MIT License — free to use, modify, and distribute for educational purposes.

---

## 🙏 Acknowledgements

Built as a demonstration project for the **Mini Secure File System** computer science challenge.  
Fonts: [Orbitron](https://fonts.google.com/specimen/Orbitron), [Rajdhani](https://fonts.google.com/specimen/Rajdhani), [Share Tech Mono](https://fonts.google.com/specimen/Share+Tech+Mono) via Google Fonts.
