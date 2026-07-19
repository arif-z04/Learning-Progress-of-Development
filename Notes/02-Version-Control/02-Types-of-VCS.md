There are **three main types of Version Control Systems (VCS)**:

---

# 1. Local Version Control System (LVCS)

###  What it is:
A system where version control is maintained **locally on a single computer**.

###  How it works:
- Files are copied to another directory.
- Changes are tracked locally using simple databases.

###  Example:
- RCS (Revision Control System)

###  Advantages:
- Simple to use
- No network required

###  Disadvantages:
- No collaboration
- Risk of losing all history if system fails
- Not suitable for team projects

---

# 2. Centralized Version Control System (CVCS)

###  What it is:
A system where there is **one central server** that stores all versions of the project.

Developers:
- Checkout files
- Make changes
- Commit changes back to the central server

###  Examples:
- SVN (Subversion)
- CVS
- Perforce

###  Advantages:
- Easier to manage
- Good for centralized teams
- Everyone sees the same version

###  Disadvantages:
- Requires network connection
- Single point of failure (if server crashes, history may be lost)
- Slower compared to distributed systems

---

# 3. Distributed Version Control System (DVCS)

###  What it is:
Each developer has a **complete copy of the repository**, including full history.

Developers can:
- Commit locally
- Work offline
- Sync with others later

###  Examples:
- Git
- Mercurial

###  Advantages:
- No single point of failure
- Faster operations
- Strong branching and merging
- Offline work possible
- Better collaboration

###  Disadvantages:
- Slightly more complex for beginners
- Larger initial clone size

---

# 🔎 Quick Comparison

| Feature | Local | Centralized | Distributed |
|----------|--------|--------------|--------------|
| Collaboration | ❌ | ✅ | ✅✅ |
| Works Offline | ✅ | ❌ | ✅ |
| Full History on Each Machine | ❌ | ❌ | ✅ |
| Speed | ✅ | ⚠️ | ✅✅ |
| Single Point of Failure | ✅ | ✅ | ❌ |

---

# Summary

- **Local VCS** → Tracks changes on one computer.
- **Centralized VCS** → One central server controls everything.
- **Distributed VCS** → Every developer has a full copy (Git).

---