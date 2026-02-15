# Mini Database Engine (C++)

A small educational database engine written in modern C++ (C++20).  
The goal is to learn systems programming fundamentals by building a simple, testable DB core step-by-step:
storage on disk, pages, a basic record format, and a minimal query layer.

> This is **not** meant to compete with real databases. It’s a learning project focused on clarity, correctness, and incremental design.

---

## Current Status

✅ Repository scaffold  
⬜ Storage layer (paged file)  
⬜ Record encoding/decoding  
⬜ Simple table format  
⬜ Minimal query execution  
⬜ Indexes (later)

---

## Roadmap (Milestones)

### M0 — Scaffold (you are here)
- CMake project layout
- unit test setup
- CI build

### M1 — Storage (Paged File)
- `Pager` that reads/writes fixed-size pages (e.g. 4KB)
- file header + page cache (optional)
- durable writes (`fsync` / flush policy later)

### M2 — Record Format
- fixed-size records first, then variable-size
- schema definition (columns, types)
- encode/decode rows

### M3 — Table Operations
- create table (metadata)
- insert row
- full scan select (no WHERE at first)

### M4 — Query Layer (Minimal)
- parse a tiny subset of SQL-like commands:
  - `CREATE TABLE`
  - `INSERT INTO`
  - `SELECT * FROM`
- execution pipeline

### M5 — Index (Optional)
- B+Tree index on one column
- point lookups and range scans

---

## Non-goals (for now)
- transactions, MVCC
- joins, optimizer
- network protocol
- full SQL compatibility

---

## Build

### Requirements
- CMake 3.22+
- C++20 compiler (Clang or GCC)

### Configure & Build
```bash
cmake -S . -B build
cmake --build build -j
````

### Run

```bash
./build/db
```

### Tests

```bash
ctest --test-dir build
```

---

## Project Structure

```
.
├─ CMakeLists.txt
├─ README.md
├─ src/
│  ├─ main.cpp
│  └─ db/
│     ├─ pager.hpp
│     ├─ pager.cpp
│     ├─ result.hpp
│     └─ ...
├─ include/
│  └─ db/
├─ tests/
│  ├─ CMakeLists.txt
│  └─ pager_tests.cpp
└─ .github/workflows/ci.yml
```

---

## Design Principles

* **Small steps**: each milestone should compile, run, and have tests.
* **RAII everywhere**: resources are owned and released automatically.
* **Explicit invariants**: clearly document file formats and page layout.
* **No premature optimization**: correctness first, performance later.

---

## License

MIT

```
