# Normalization

---

## What is Normalization?

**Normalization** is the process of organizing a database to:
- Reduce **data redundancy** (repeated data)
- Improve **data integrity**
- Make the database more **efficient**

In simple words:

> Normalization is the process of **breaking down a large, poorly designed table** into smaller, well-structured tables.

Introduced by **E.F. Codd** along with the Relational Model.

---

## Why Normalization?

Consider this table:

| StudentID | StudentName | CourseID | CourseName | Instructor | InstructorPhone |
|-----------|------------|----------|------------|------------|-----------------|
| 1 | Alice | C01 | Database | Dr. Smith | 01711 |
| 1 | Alice | C02 | Networking | Dr. Jones | 01811 |
| 2 | Bob | C01 | Database | Dr. Smith | 01711 |
| 3 | Charlie | C02 | Networking | Dr. Jones | 01811 |

### Problems in this table:

| Problem | Description | Example |
|---------|-------------|---------|
| **Data Redundancy** | Same data repeated multiple times | Dr. Smith and 01711 repeated |
| **Update Anomaly** | Updating one record requires updating many | Changing Dr. Smith's phone in multiple rows |
| **Insertion Anomaly** | Cannot add data without other data | Cannot add a course without a student |
| **Deletion Anomaly** | Deleting one record removes other useful data | Deleting Charlie removes Networking course info |

Normalization solves all these problems.

---

## Anomalies Explained

```mermaid
graph TD
    A[Problems Without Normalization] --> B[Data Redundancy\nSame data repeated]
    A --> C[Update Anomaly\nMust update multiple rows]
    A --> D[Insertion Anomaly\nCannot insert partial data]
    A --> E[Deletion Anomaly\nDeleting removes useful data]

    style A fill:#e74c3c,stroke:#333,stroke-width:2px,color:#fff
    style B fill:#e67e22,stroke:#333,stroke-width:2px,color:#fff
    style C fill:#e67e22,stroke:#333,stroke-width:2px,color:#fff
    style D fill:#e67e22,stroke:#333,stroke-width:2px,color:#fff
    style E fill:#e67e22,stroke:#333,stroke-width:2px,color:#fff
```

---

## Normal Forms

Normalization is done step by step through **Normal Forms**.

```mermaid
graph LR
    A[Unnormalized\nTable] --> B[1NF]
    B --> C[2NF]
    C --> D[3NF]
    D --> E[BCNF]

    style A fill:#e74c3c,stroke:#333,stroke-width:2px,color:#fff
    style B fill:#e67e22,stroke:#333,stroke-width:2px,color:#fff
    style C fill:#f39c12,stroke:#333,stroke-width:2px,color:#fff
    style D fill:#27ae60,stroke:#333,stroke-width:2px,color:#fff
    style E fill:#3498db,stroke:#333,stroke-width:2px,color:#fff
```

Each normal form has a set of rules. A table must satisfy all previous rules before moving to the next level.

---

## 1NF — First Normal Form

### Rules
- Every column must have **atomic (single) values**
- No **repeating groups** or arrays in a column
- Each column must have a **unique name**
- Each row must be **unique**

### Problem Table (Not in 1NF)

| StudentID | Name | Courses |
|-----------|------|---------|
| 1 | Alice | Database, Networking |
| 2 | Bob | Database |

**Problem:** Courses column has multiple values in one cell → Not atomic.

### After 1NF

| StudentID | Name | Course |
|-----------|------|--------|
| 1 | Alice | Database |
| 1 | Alice | Networking |
| 2 | Bob | Database |

> Each cell now has only one value → **1NF achieved** ✅

---

## Functional Dependency

Before understanding 2NF and 3NF, we need to understand **Functional Dependency**.

### Definition
If the value of attribute **A** determines the value of attribute **B**, then **B is functionally dependent on A**.

### Notation
```
A → B
(A determines B)
```

### Example

| StudentID | Name |
|-----------|------|
| 1 | Alice |
| 2 | Bob |

StudentID → Name

> Knowing StudentID, we can determine the Name.

---

## 2NF — Second Normal Form

### Rules
- Table must already be in **1NF**
- Every non-key attribute must be **fully functionally dependent** on the **entire primary key**
- No **partial dependency** allowed

### What is Partial Dependency?

When a non-key attribute depends on **only part** of the composite primary key (not the whole key).

### Problem Table (Not in 2NF)

Primary Key = **(StudentID + CourseID)**

| StudentID | CourseID | StudentName | CourseName |
|-----------|----------|-------------|------------|
| 1 | C01 | Alice | Database |
| 1 | C02 | Alice | Networking |
| 2 | C01 | Bob | Database |

**Partial Dependencies:**
- StudentName depends only on **StudentID** (not CourseID)
- CourseName depends only on **CourseID** (not StudentID)

This is **partial dependency** → Not in 2NF.

### After 2NF — Split into 3 tables

**Students Table:**

| StudentID | StudentName |
|-----------|-------------|
| 1 | Alice |
| 2 | Bob |

**Courses Table:**

| CourseID | CourseName |
|----------|------------|
| C01 | Database |
| C02 | Networking |

**Enrollment Table:**

| StudentID | CourseID |
|-----------|----------|
| 1 | C01 |
| 1 | C02 |
| 2 | C01 |

> Partial dependency removed → **2NF achieved** ✅

---

## 3NF — Third Normal Form

### Rules
- Table must already be in **2NF**
- No **transitive dependency** allowed

### What is Transitive Dependency?

When a non-key attribute depends on **another non-key attribute** (instead of the primary key directly).

```
Primary Key → Non-key A → Non-key B
```

B is transitively dependent on the Primary Key through A.

### Problem Table (Not in 3NF)

| StudentID | Name | DeptID | DeptName |
|-----------|------|--------|----------|
| 1 | Alice | 101 | CSE |
| 2 | Bob | 102 | Math |
| 3 | Charlie | 101 | CSE |

**Transitive Dependency:**

```
StudentID → DeptID → DeptName
```

DeptName depends on DeptID, not directly on StudentID.

### After 3NF — Split into 2 tables

**Students Table:**

| StudentID | Name | DeptID |
|-----------|------|--------|
| 1 | Alice | 101 |
| 2 | Bob | 102 |
| 3 | Charlie | 101 |

**Departments Table:**

| DeptID | DeptName |
|--------|----------|
| 101 | CSE |
| 102 | Math |

> Transitive dependency removed → **3NF achieved** ✅

---

## BCNF — Boyce-Codd Normal Form

### Definition
BCNF is a **stricter version** of 3NF.

### Rule
- Table must already be in **3NF**
- For every functional dependency **A → B**, A must be a **super key**

### When does 3NF fail?

3NF allows some anomalies when there are **multiple overlapping candidate keys**.

### Problem Table (in 3NF but not BCNF)

A student can have multiple teachers per subject.  
Each teacher teaches only one subject.

| StudentID | Subject | Teacher |
|-----------|---------|---------|
| 1 | Database | Dr. Smith |
| 1 | Networking | Dr. Jones |
| 2 | Database | Dr. Smith |

**Candidate Keys:** (StudentID + Subject) or (StudentID + Teacher)

**Problem:**
```
Teacher → Subject
```
Teacher is not a super key but determines Subject → BCNF violated.

### After BCNF — Split into 2 tables

**Teacher Subject Table:**

| Teacher | Subject |
|---------|---------|
| Dr. Smith | Database |
| Dr. Jones | Networking |

**Student Teacher Table:**

| StudentID | Teacher |
|-----------|---------|
| 1 | Dr. Smith |
| 1 | Dr. Jones |
| 2 | Dr. Smith |

> BCNF violation removed → **BCNF achieved** ✅

---

## Summary of Normal Forms

| Normal Form | Rule | Removes |
|------------|------|---------|
| **1NF** | Atomic values, no repeating groups | Multi-valued cells |
| **2NF** | No partial dependency | Partial dependency on composite key |
| **3NF** | No transitive dependency | Dependency between non-key attributes |
| **BCNF** | Every determinant must be a super key | Anomalies left by 3NF |

---

## Normalization Flow with Example

```mermaid
flowchart TD
    A[Original Messy Table\nAll data in one table] --> B[1NF\nAtomic values only]
    B --> C[2NF\nRemove Partial Dependency]
    C --> D[3NF\nRemove Transitive Dependency]
    D --> E[BCNF\nEvery determinant is a Super Key]

    style A fill:#e74c3c,stroke:#333,stroke-width:2px,color:#fff
    style B fill:#e67e22,stroke:#333,stroke-width:2px,color:#fff
    style C fill:#f39c12,stroke:#333,stroke-width:2px,color:#fff
    style D fill:#27ae60,stroke:#333,stroke-width:2px,color:#fff
    style E fill:#3498db,stroke:#333,stroke-width:2px,color:#fff
```

---

## Advantages of Normalization

- ✅ Removes data redundancy
- ✅ Eliminates update, insertion, and deletion anomalies
- ✅ Improves data consistency and integrity
- ✅ Makes the database easier to maintain

## Disadvantages of Normalization

- ❌ More tables mean more **JOIN operations** which can slow down queries
- ❌ Database design becomes more **complex**
- ❌ May reduce performance for **read-heavy** applications

---

## Summary

- **Normalization** is the process of organizing a database to reduce redundancy and improve data integrity.
- It is done through **Normal Forms** — 1NF, 2NF, 3NF, BCNF.
- **1NF** — Atomic values only.
- **2NF** — No partial dependency.
- **3NF** — No transitive dependency.
- **BCNF** — Every determinant must be a super key.
- Each level builds on the previous one and removes a specific type of problem.


# 4NF and 5NF

---

## Quick Recap

So far in normalization:

| Normal Form | Removes |
|------------|---------|
| 1NF | Multi-valued cells |
| 2NF | Partial Dependency |
| 3NF | Transitive Dependency |
| BCNF | Determinant that is not a Super Key |
| **4NF** | **Multi-valued Dependency** |
| **5NF** | **Join Dependency** |

---

## 4NF — Fourth Normal Form

### Definition

A table is in **4NF** if:
- It is already in **BCNF**
- It has **no multi-valued dependency**

---

### What is Multi-Valued Dependency?

A **Multi-Valued Dependency** occurs when one attribute in a table **independently determines multiple values** of two other attributes.

### Notation
```
A →→ B
(A multi-determines B)
```

This means: For a single value of A, there are **multiple independent values** of B.

---

### Example — Problem Table (Not in 4NF)

Consider a table where a student can have multiple hobbies and multiple courses — **independently** of each other.

| StudentID | Hobby | Course |
|-----------|-------|--------|
| 1 | Cricket | Database |
| 1 | Cricket | Networking |
| 1 | Reading | Database |
| 1 | Reading | Networking |
| 2 | Football | Database |
| 2 | Football | Networking |

**Multi-Valued Dependencies:**
```
StudentID →→ Hobby
StudentID →→ Course
```

Hobbies and Courses are **independent** of each other but both depend on StudentID.

### Problems

- If student 1 adds a new hobby **Gaming**, we must add:
  - (1, Gaming, Database)
  - (1, Gaming, Networking)
  - → **Insertion Anomaly**

- If student 1 drops Networking course, we must delete multiple rows → **Deletion Anomaly**

---

### After 4NF — Split into 2 tables

**Student Hobbies Table:**

| StudentID | Hobby |
|-----------|-------|
| 1 | Cricket |
| 1 | Reading |
| 2 | Football |

**Student Courses Table:**

| StudentID | Course |
|-----------|--------|
| 1 | Database |
| 1 | Networking |
| 2 | Database |
| 2 | Networking |

> Multi-valued dependency removed → **4NF achieved** ✅

Now hobbies and courses are stored **independently**. Adding a new hobby does not require adding new course rows.

---

### 4NF Rule Summary

| Check | Condition |
|-------|-----------|
| Must be in BCNF | ✅ |
| No multi-valued dependency | ✅ |

---

## 5NF — Fifth Normal Form

### Definition

A table is in **5NF** if:
- It is already in **4NF**
- It has **no join dependency**

5NF is also called **Project-Join Normal Form (PJNF)**.

---

### What is Join Dependency?

A **Join Dependency** exists when a table can be **split into multiple smaller tables** and then **joined back** to get the original table **without losing any data** and **without generating extra rows**.

In simple words:

> If a table can be **perfectly reconstructed** by joining its decomposed tables, it has a join dependency.

If this decomposition is **not lossless** (generates extra rows), then 5NF is violated.

---

### Example — Problem Table (Not in 5NF)

Consider this table:
- A supplier supplies certain parts
- A supplier is associated with a project
- A part is used in a project

| Supplier | Part | Project |
|----------|------|---------|
| S1 | P1 | J1 |
| S1 | P2 | J2 |
| S2 | P1 | J1 |
| S2 | P2 | J1 |

This table has a **join dependency**. It can only be correctly represented by keeping all three attributes together.

If we split into two tables and join them back, we may get **extra (spurious) rows** that did not exist originally.

---

### After 5NF — Split into 3 tables

**Supplier Part Table:**

| Supplier | Part |
|----------|------|
| S1 | P1 |
| S1 | P2 |
| S2 | P1 |
| S2 | P2 |

**Supplier Project Table:**

| Supplier | Project |
|----------|---------|
| S1 | J1 |
| S1 | J2 |
| S2 | J1 |

**Part Project Table:**

| Part | Project |
|------|---------|
| P1 | J1 |
| P2 | J2 |
| P1 | J1 |
| P2 | J1 |

Joining all three tables back gives the **exact original table** with no extra rows.

> Join dependency removed → **5NF achieved** ✅

---

### 5NF Rule Summary

| Check | Condition |
|-------|-----------|
| Must be in 4NF | ✅ |
| No join dependency | ✅ |
| Lossless decomposition | ✅ |

---

## 4NF vs 5NF

| Feature | 4NF | 5NF |
|---------|-----|-----|
| Based On | BCNF | 4NF |
| Removes | Multi-Valued Dependency | Join Dependency |
| Also Called | - | PJNF (Project-Join Normal Form) |
| Complexity | Moderate | Most Complex |
| How Common | Occasionally needed | Rarely needed in practice |

---

## Complete Normalization Flow

```mermaid
flowchart TD
    A[Unnormalized Table] --> B[1NF\nAtomic Values]
    B --> C[2NF\nNo Partial Dependency]
    C --> D[3NF\nNo Transitive Dependency]
    D --> E[BCNF\nDeterminant must be Super Key]
    E --> F[4NF\nNo Multi-Valued Dependency]
    F --> G[5NF\nNo Join Dependency]

    style A fill:#e74c3c,stroke:#333,stroke-width:2px,color:#fff
    style B fill:#e67e22,stroke:#333,stroke-width:2px,color:#fff
    style C fill:#f39c12,stroke:#333,stroke-width:2px,color:#fff
    style D fill:#27ae60,stroke:#333,stroke-width:2px,color:#fff
    style E fill:#3498db,stroke:#333,stroke-width:2px,color:#fff
    style F fill:#9b59b6,stroke:#333,stroke-width:2px,color:#fff
    style G fill:#1abc9c,stroke:#333,stroke-width:2px,color:#fff
```

---

## Complete Summary of All Normal Forms

| Normal Form | Rule | Removes | Example Problem |
|------------|------|---------|-----------------|
| **1NF** | Atomic values | Multi-valued cells | Courses: Database, Networking in one cell |
| **2NF** | No partial dependency | Partial dependency on composite key | StudentName depends only on StudentID |
| **3NF** | No transitive dependency | Non-key to non-key dependency | DeptName depends on DeptID not StudentID |
| **BCNF** | Every determinant is a super key | Overlapping candidate key anomalies | Teacher → Subject but Teacher is not super key |
| **4NF** | No multi-valued dependency | Independent multi-valued facts in one table | StudentID →→ Hobby, StudentID →→ Course |
| **5NF** | No join dependency | Lossless join decomposition issues | Supplier, Part, Project combination |

---

## Summary

- **4NF** deals with **Multi-Valued Dependency**.
  - When one attribute independently determines multiple values of two other attributes.
  - Solution: Split the table into separate tables for each multi-valued fact.

- **5NF** deals with **Join Dependency**.
  - When a table can be split into smaller tables and joined back perfectly.
  - Solution: Decompose into smallest possible tables without losing information.

- In practice, most databases are normalized up to **3NF or BCNF**.
- **4NF and 5NF** are applied in highly complex databases where data anomalies still exist after BCNF.