# Library Management System (C++)

Simple console-based Library Management System implemented in C++. It provides basic functionality to manage a small library using plain text files for storage.

## Features
- Add / remove books (admin)
- Display catalogue
- Patron signup / login
- Request book if unavailable
- Checkout / return books (updates `books.txt` and `checkedoutBooks.txt`)
- Notification centre for pending requests
- Simple binary search tree (BST) lookup by book ID
- Keeps lightweight admin activity history in memory

## Files in this repository
- `LIBRARY_MANAGEMENT_SYSTEM.cpp` — main source file (single-file project)
- `LIBRARY_MANAGEMENT_SYSTEM.sln` — Visual Studio solution (optional)
- `books.txt` — persisted catalogue (tab-separated values: id, title, author, availability)
- `checkedoutBooks.txt` — persisted checkout records (patronId \t bookId)
- `patrons.txt` — persisted patrons (name \t id)

## Requirements
- Windows (project includes `<Windows.h>` calls and uses `system("CLS")` and `system("pause")`)
- Visual Studio or any C++ compiler that targets Windows (MSVC, MinGW)
- C++11/C++17 compatible compiler

## Build & Run (Windows)
### Visual Studio
1. Open `LIBRARY_MANAGEMENT_SYSTEM.sln` in Visual Studio.
2. Build and run the solution (Ctrl+F5 to run without debugging).

### g++ (MinGW) — PowerShell example
Note: If you use MinGW, Windows-specific behaviour (console clear/pause and `Windows.h`) may differ.

PS> g++ -std=c++17 -O2 -o LibraryManagement.exe LIBRARY_MANAGEMENT_SYSTEM.cpp
PS> .\LibraryManagement.exe

## Usage
- On start the app shows a logo and asks to login as Admin or Student.
- Admin:
  - Password: `admin123`
  - Can add/remove books and view history.
  - When adding a book it appends to `books.txt`.
- Student:
  - Can sign up (writes to `patrons.txt`) and login using the ID.
  - Can checkout available books, request unavailable ones, view and return checked-out books, and search by book ID.

Notes about files and formats:
- `books.txt` uses: `id\ttitle\tauthor\tavailability` where availability is `1` (true) or `0` (false).
- `patrons.txt` uses: `name id` per line.
- `checkedoutBooks.txt` stores lines: `patronId\tbookId` (appended on checkout).

## Important developer notes
- The project currently tracks admin history and checkout history in memory (stacks); these are not persisted across runs.
- The code contains Windows-specific calls (`Windows.h`, `system("CLS")`, `system("pause")`). If targeting other OSes remove or adapt those parts.
- The project currently ships as a single large source file. Consider splitting into headers and implementation files for maintainability.

## Git / Repository advice
- Do NOT commit generated IDE files or temporary build artifacts (Visual Studio `.vs/` folder, `.user`, `ipch`, `*.obj`, `*.exe`, etc.).
- Add a `.gitignore` at repo root with at least the following lines:

```
# Visual Studio
.vs/
*.suo
*.user
ipch/
*.ipch
*.obj
*.exe
*.log

# Build artifacts
build/

# Rider/Other IDEs
.idea/
```

- If you already committed a large file (e.g. `.vs/.../*.ipch`) and the push was rejected by GitHub due to the 100 MB limit, remove it from Git history before pushing. Two quick approaches:
  - If the large file is only in the most recent commit:

```powershell
# add .vs/ to .gitignore
".vs/" | Out-File -Encoding utf8 -Append .gitignore
# remove file from index
git rm --cached ".vs/YourSolution/v17/ipch/.../bigfile.ipch"
# amend commit and force-push
git add .gitignore
git commit --amend --no-edit
git push --force origin main
```

  - For removing files across history, use BFG Repo-Cleaner or `git filter-repo`. Rewriting history requires force-push and coordination with collaborators.
- Alternatively, use Git LFS for large binary assets but converting existing tracked files to LFS also requires history cleanup.

## Contributors
- Muhammad Hamza (22K-4523)
- Saad Arshad (22K-4141)
- Abdul Wasey (22K-4172)

## License
This repository contains student project code. Add a license if you want to permit reuse.


If you want, I can add a `.gitignore` file and/or remove the large tracked file from your Git history — tell me which option you prefer.
