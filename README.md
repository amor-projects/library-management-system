# 📚 Library Management System

![Build](https://img.shields.io/badge/Build-Console%20App-2EA44F?style=for-the-badge&logo=gradle&logoColor=white)
![Language](https://img.shields.io/badge/Language-Java-007396?style=for-the-badge&logo=java&logoColor=white)
![Status](https://img.shields.io/badge/Status-Active-3FB950?style=for-the-badge&logo=githubactions&logoColor=white)
![Focus](https://img.shields.io/badge/Focus-OOP%20Design-F59E0B?style=for-the-badge&logo=codacy&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-64748B?style=for-the-badge&logo=opensourceinitiative&logoColor=white)

## 🎓 University Library Management System 

## ✨ Description
I am building a university-level library system that manages books, members, borrowing rules, reservations, and fines. It models realistic academic policies with clearly defined roles and book categories.

> I am building a mid-sized university library, not a national archive.

---

## 👥 User Roles (Exactly 3)

1. Student
2. Faculty
3. Guest

That’s it. No admin role as a borrower. Admin is a system operator, not a borrowing entity.

## 📦 Borrowing Rules

### Student
- Max 5 active borrowings
- Loan duration: 14 days
- Fine: $1 per day overdue
- Can reserve books

### Faculty
- Max 10 active borrowings
- Loan duration: 30 days
- Fine: $0.50 per day overdue
- Can reserve books
- Can borrow reference books (in-library use only, 6-hour limit)

### Guest
- Max 2 active borrowings
- Loan duration: 7 days
- Fine: $2 per day overdue
- Cannot reserve books
- Cannot borrow reference books

> These rules are fixed.

---

## 📚 Book Types (Exactly 4)

1. PhysicalBook
2. EBook
3. AudioBook
4. ReferenceBook

## 🧭 Definitions

**PhysicalBook**
- Has limited copies
- Can be borrowed normally
- Can be reserved

**EBook**
- Unlimited copies
- No reservation required
- Borrowed digitally
- No physical return processing

**AudioBook**
- Unlimited copies
- Same rules as EBook
- Borrowed digitally

**ReferenceBook**
- Physical only
- Exactly 1 copy
- Cannot be borrowed normally
- Faculty can check out for 6 hours (in-library use)
- Students and Guests cannot borrow

_**Important design decision:**_

> ReferenceBook is **NOT** also an ebook or audiobook. It is a separate physical-only category. No hybrid types. Keep taxonomy clean.

---

## ✅ Core Features (Mandatory)

- Add/remove books
- Register/remove members
- Borrow book
- Return book
- Reserve physical book (queue-based)
- Automatic fine calculation
- Track due dates
- Track book status (Available, Borrowed, Reserved, InLibraryUse)
- Prevent rule violations (limit exceeded, restricted access, etc.)
- File-based persistence (simple serialization or structured text)

---

## 🧩 State Rules (No ambiguity)

### PhysicalBook states
- Available → Borrowed → Available
- Available → Reserved → Borrowed
- Borrowed → Reserved (queue exists)

### EBook & AudioBook states
- Always Available
- Borrowed status tracked per user, not per copy

### ReferenceBook states
- Available → InLibraryUse → Available

> No other states allowed.

---

## 🗓️ Reservation Rules

- Only PhysicalBook can be reserved
- FIFO queue
- When returned, automatically assign to first user in queue
- Guest cannot reserve

---

## 💸 Fine Rules

- Fine = (CurrentDate - DueDate) × RoleRate
- No compound logic.
- Fine accumulates until paid.

> Users with unpaid fines above $20 cannot borrow.

---

## 🏁 Success Criteria

**The system is successful if:**

- Adding a new role would require minimal modification
- Borrowing rules are not hardcoded in a giant conditional block
- Book type behavior differs without if-else chains everywhere
- State transitions are validated and cannot enter invalid states
- Persistence works across restarts
- Edge cases do not break the system

---

## 🚫 What I Am Not Building

- GUI
- Database
- Networked system
- Multi-branch library
- Payment gateway
- Search engine ranking

> I stay focused.

---

**If I build exactly this specification, I will encounter:**

- Inheritance decisions
- Polymorphism decisions
- State modeling
- Rule encapsulation
- Separation of concerns
- Basic persistence architecture

---

#### ✨ Built with Passion
<div style="display: flex; place-content: center">
Crafted with 💖  by 
 <a href="https://github.com/ZephyrAmmor"><img style="margin-left: 8px; display: block" alt="Zephyr Ammor Github Account" src="https://img.shields.io/badge/GitHub-ZephyrAmmor-181717?style=for-the-badge&logo=github&logoColor=white)" /></a>
</div>

> **_A NEW BEGINNING_**
---
