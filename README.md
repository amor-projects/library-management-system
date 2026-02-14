## LIBRARY MANAGEMENT SYSTEM

### University Library Management System (Console-Based)

### Description
A university-level library system that manages books, members, borrowing rules, reservations, and fines. The system models realistic academic policies with clearly defined roles and book categories.

> You are building a mid-sized university library, not a national archive.

---

### USER ROLES (Exactly 3)

1. Student
2. Faculty
3. Guest

That’s it. No admin role as a borrower. Admin is a system operator, not a borrowing entity.

### Borrowing Rules:

#### Student
- Max 5 active borrowings
- Loan duration: 14 days
- Fine: $1 per day overdue
- Can reserve books

#### Faculty
- Max 10 active borrowings
- Loan duration: 30 days
- Fine: $0.50 per day overdue
- Can reserve books
- Can borrow reference books (in-library use only, 6-hour limit)

#### Guest
- Max 2 active borrowings
- Loan duration: 7 days
- Fine: $2 per day overdue
- Cannot reserve books
- Cannot borrow reference books

> These rules are fixed.

---

### BOOK TYPES (Exactly 4)

1. PhysicalBook
2. EBook
3. AudioBook
4. ReferenceBook

#### Definitions:

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

### CORE FEATURES (Mandatory)

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

### STATE RULES (No ambiguity)

#### PhysicalBook states:
- Available → Borrowed → Available
- Available → Reserved → Borrowed
- Borrowed → Reserved (queue exists)

#### EBook & AudioBook states:
- Always Available
- Borrowed status tracked per user, not per copy

#### ReferenceBook states:
- Available → InLibraryUse → Available

> No other states allowed.

---

### RESERVATION RULES

- Only PhysicalBook can be reserved
- FIFO queue
- When returned, automatically assign to first user in queue
- Guest cannot reserve

---

### FINE RULES

- Fine = (CurrentDate - DueDate) × RoleRate
- No compound logic.
- Fine accumulates until paid.

> Users with unpaid fines above $20 cannot borrow.

---

### SUCCESS CRITERIA

**The system is successful if:**

- Adding a new role would require minimal modification
- Borrowing rules are not hardcoded in a giant conditional block
- Book type behavior differs without if-else chains everywhere
- State transitions are validated and cannot enter invalid states
- Persistence works across restarts
- Edge cases do not break the system

---

### WHAT YOU ARE NOT BUILDING

- GUI
- Database
- Networked system
- Multi-branch library
- Payment gateway
- Search engine ranking

> Stay focused.

---

**If you build exactly this specification, you will encounter:**

- Inheritance decisions
- Polymorphism decisions
- State modeling
- Rule encapsulation
- Separation of concerns
- Basic persistence architecture
> **_A NEW BEGINNING_**
---
