# Secure User File Vault (SUFV)
A console-based C++ application for authenticated personal file storage, backed by a PostgreSQL database with Argon2id password hashing and per-user file isolation.

## Features
- Secure user registration and login with Argon2id password hashing (memory-hard, industry standard)
- Per-user file isolation enforced at the database level — users can never access each other's files
- Import existing files or create new ones (`.txt`, `.docx`, `.pptx`, `.xlsx`) directly from the vault
- Files opened in native OS applications (Notepad, Word, PowerPoint, Excel) and saved back to the database
- Automatic cleanup of temporary files using RAII — no leftover files even on crash or early exit
- Password recovery via hashed security question
- SQL injection prevention via prepared statements throughout

## Tech Stack
- **Language:** C++17
- **Database:** PostgreSQL (via libpqxx)
- **Hashing:** Argon2id (libargon2)
- **Crypto RNG:** OpenSSL `RAND_bytes`
- **Platform:** Windows (Win32 API — `ShellExecuteEx`, `GetOpenFileName`, `GetTempPath`)
- **Compiler:** GCC via MSYS2/UCRT64

## How to Run

1. Install dependencies: MSYS2/UCRT64 with GCC, libpqxx, libargon2, OpenSSL, and a running PostgreSQL instance on port 5433
2. Set your database password as an environment variable:
   ```
   set DB_PASS=your_database_password
   ```
3. Compile:
   ```
   g++ sufv.cpp -o sufv -lpqxx -lpq -largon2 -lssl -lcrypto -lcomdlg32 -lshell32
   ```
4. Place `text.txt`, `thankyou.txt`, and `face.txt` (ASCII art assets) in the same directory as the executable
5. Run:
   ```
   ./login
   ```

## My Role and AI Assistance

**Code:** Written by me; I used an AI assistant for research, clarification of concepts, and feedback on design decisions. All implementation and debugging were done manually.

**Technical report** (AI-generated draft): The initial draft of this technical report was generated with the help of an AI assistant and then revised, fact-checked, and edited by me.

---
*This project was created as part of my BTech coursework in Year 1.*
