# Justin Christopher
### SNHU Computer Science | CS 499 Capstone ePortfolio

---

## Professional Self-Assessment

Completing the Computer Science program at Southern New Hampshire University over the past three years has given me both a technical foundation and a professional perspective on what it means to build software that works for real users. When I started the program, I thought of development mostly in terms of making something appear on a screen. By the time I reached this capstone, my thinking had expanded to include how data is structured, how access is controlled, how code is organized so other developers can work with it, and how a system should behave when something goes wrong. This ePortfolio is the result of that growth, built around a single artifact (an Android inventory management application from CS 360) that I enhanced across three categories to demonstrate the range of skills I developed throughout the program.

### Collaborating in a Team Environment

Although the capstone project was completed independently, my coursework gave me experience learning about collaborative settings. In CS 250: Software Development Lifecycle, I learned how Agile teams plan and execute sprints, communicate through standups, and use retrospectives to improve their process. In CS 320: Software Testing, Automation, and Quality Assurance, I practiced writing tests that would be meaningful not just to me but to anyone maintaining the codebase after me. These experiences shaped how I approach code even when working solo. I write comments that explain decisions rather than restating what the code does, I use consistent naming conventions, and I organize my commits so another developer could follow the history. The code review I produced for this capstone reflects that same mindset: I walked through the codebase as if explaining it to a teammate, identifying issues and proposing improvements in a structured, professional format.

### Communicating with Stakeholders

Effective communication has been a recurring theme across the program. The narratives that accompany each enhancement in this portfolio are written for a mixed audience, technically detailed enough for a developer to follow the reasoning but clear enough for a non-technical stakeholder to understand the value of each change. Throughout my coursework I learned to translate technical architecture into descriptions that a project manager or client could evaluate. That skill shows up directly in this capstone through the code review video, the enhancement narratives, and this self-assessment, all of which are designed to make my work accessible to different audiences.

### Data Structures and Algorithms

My understanding of data structures and algorithms deepened throughout the program and was applied directly in Enhancement Two of this portfolio. The original inventory app loaded every record from the database into memory and displayed them in a fixed alphabetical order with no way to search or filter. I refactored the data retrieval logic to accept dynamic query parameters, built a `searchItems()` method in the database helper that constructs SQL `WHERE` clauses using `LIKE` for name filtering and quantity conditions for low-stock filtering, and added a search bar and filter controls to the UI. This pushed filtering to the database engine rather than performing it in Java, which is the more efficient approach as the dataset grows. The enhancement required evaluating trade-offs between simplicity and performance, a skill that CS 340 and other coursework emphasized.

### Software Engineering and Databases

Software engineering and database design are tightly connected in this portfolio because the enhancements I made in those categories depended on each other. Enhancement One introduced a role-based access control system where new accounts start as "pending" and require administrator approval before the user can access inventory data. Enhancement Three expanded the SQLite schema to support that system, adding `role`, `account_status`, and `can_edit` columns to the users table and building the corresponding CRUD methods. Working on these two enhancements together taught me that database decisions are not just storage decisions. They shape the security model, the UI logic, and the overall architecture of the application. Courses like DAD 220 and CS 340 gave me the SQL and data modeling foundations that made this work possible.

### Security

Developing a security mindset was one of the most important outcomes of the program for me. The original inventory app stored passwords in plain text, gave every registered user immediate full access, and had a hardcoded phone number embedded in the source code. In my code review, I identified these as vulnerabilities and proposed specific mitigations. The enhanced version implements administrator-controlled account approval, permission-based access (read-only versus write), and removes the hardcoded phone number. The OWASP Code Review Guide influenced my approach, specifically the idea that a secure review goes beyond asking how code works and asks how it could be misused. That principle guided every enhancement I made.

### Portfolio Summary

The three enhancements in this portfolio work together to transform a functional course prototype into something closer to a production-ready business application. Enhancement One (Software Engineering and Design) adds the access control layer. Enhancement Three (Databases) provides the schema foundation that makes that access control possible. Enhancement Two (Algorithms and Data Structures) improves how users interact with the data once they have access. Together, they demonstrate that I can design, build, and reason about a complete software system rather than just individual features in isolation.

---

## Artifact Overview: Inventory Management App (CS 360)

This Android application was originally built in CS 360: Mobile Architecture and Programming. It is designed to help a business track inventory levels. The app features a login screen where users can log in or create an account, and an inventory management screen where items and their quantities are displayed in a scrollable list. Rows highlight red when an item drops below its configured low-stock threshold, and the app includes optional SMS notifications for low-stock alerts.

**Technologies:** Java, Android SDK (Android Studio), SQLite, XML layouts

The original source code and all enhanced versions are available in the GitHub repository linked at the bottom of this page.

---

## Enhancement One: Software Engineering and Design

**Course Outcome Alignment:** Outcome 2 (Professional Communication) and Outcome 5 (Security Mindset)

### What Changed

The original application allowed any user to create an account and immediately gain full access to all inventory data. There was no distinction between user roles, no approval process, and no way to restrict what a logged-in user could do.

This enhancement adds a role-based access control system with an administrator approval workflow. When a new user registers, their account is created with a "pending" status and they cannot access the inventory screen until an administrator approves them. A default administrator account is seeded when the database is first created so the workflow is testable from the first install. The administrator has access to a dedicated admin screen where they can view pending accounts and either approve or deny them. Approved users can be assigned read-only or write permissions. Read-only users can view the inventory but cannot add, edit, or delete items, while write users have full access.

### Why It Matters

This enhancement demonstrates a security mindset by anticipating how unrestricted account access could be exploited in a real business environment. Organizations do not want every employee to have the ability to modify inventory records, and an approval workflow ensures that access is intentional rather than automatic. The enhancement also demonstrates software design skills because adding roles and permissions required changes across the database layer, the login flow, the inventory screen, and a new admin activity, all of which needed to work together coherently.

[View the full Enhancement One narrative (PDF)](https://github.com/JustinChristopher2097/JustinChristopher2097.github.io/blob/main/narratives/Enhancement1_Narrative.pdf)

---

## Enhancement Two: Algorithms and Data Structures

**Course Outcome Alignment:** Outcome 3 (Algorithmic Problem Solving)

### What Changed

The original application displayed all inventory items in a fixed alphabetical order. There was no way to search for a specific item by name or filter the list to show only items that were low on stock. The `loadData()` method retrieved every row from the database and passed the full list to the adapter with no filtering logic.

This enhancement adds a search bar and a low-stock filter toggle to the inventory screen. As the user types in the search bar, the list updates in real time to show only items whose names match the input. The low-stock filter, when enabled, shows only items whose quantity is at or below their configured threshold. Under the hood, the `loadData()` method was refactored to call a new `searchItems()` method in the database helper, which builds a dynamic SQL `WHERE` clause using `LIKE` for name matching and a quantity condition for the low-stock filter. This pushes all filtering to the database engine rather than loading every record into memory and filtering in Java.

### Why It Matters

This enhancement demonstrates the ability to design efficient computing solutions using algorithmic principles. Filtering at the database level rather than in application memory is the more scalable approach. As the inventory grows, the database engine handles the filtering work instead of the app iterating over an increasingly large list. The enhancement also required modifying how data flows through the application, from the UI input to the query construction to the adapter update, which demonstrates understanding of data structures and application architecture.

[View the full Enhancement Two narrative (PDF)](https://github.com/JustinChristopher2097/JustinChristopher2097.github.io/blob/main/narratives/Enhancement2_Narrative.pdf)

---

## Enhancement Three: Databases

**Course Outcome Alignment:** Outcome 3 (Algorithmic Problem Solving)

### What Changed

The original database schema contained a users table with only three columns: `id`, `username`, and `password`. Any registered user was immediately granted full access. The items table was functional but the users table had no support for roles, permissions, or account status.

This enhancement expands the users table to include three new columns: `role` (storing "admin" or "user"), `account_status` (storing "pending", "approved", or "denied"), and `can_edit` (a boolean flag for write access). New CRUD methods were added to `DBhelper` to support these fields. The `getUserStatus()` method checks whether an account is approved before login is allowed, `approveUser()` and `denyUser()` let the admin control access, `setPermission()` toggles the write flag, and `getRole()` determines what UI elements to show. The database version was incremented from 1 to 2, and `onUpgrade()` was updated to handle migration. A default admin account is seeded on first install.

### Why It Matters

This enhancement demonstrates applied knowledge of database design and the ability to evolve a schema to meet new application requirements without breaking existing functionality. Adding `role` and `account_status` as separate columns rather than combining them into a single field was a deliberate design trade-off. It makes the data more queryable and the application logic easier to reason about. The `searchItems()` method added in Enhancement Two also reflects database-level thinking, since it pushes filtering into SQL rather than performing it in Java. Together, these changes show that I can design a schema intentionally and extend it as requirements change.

[View the full Enhancement Three narrative (PDF)](https://github.com/JustinChristopher2097/JustinChristopher2097.github.io/blob/main/narratives/Enhancement3_Narrative.pdf)

---

## Code Review

Before making any enhancements, I recorded a code review walkthrough that covers the existing functionality, identifies areas for improvement across all three categories, and presents the planned enhancements with their course outcome alignments.

[Watch the Code Review Video on YouTube](https://youtu.be/nmRJlyeZYAA)

---

## Source Code

**Original artifact:** [Original CS 360 Inventory App](https://github.com/JustinChristopher2097/JustinChristopher2097.github.io/tree/main/original)

**Enhanced artifact:** [Enhanced Inventory App with all three enhancements](https://github.com/JustinChristopher2097/JustinChristopher2097.github.io/tree/main/enhanced)

**GitHub Repository:** [github.com/JustinChristopher2097/JustinChristopher2097.github.io](https://github.com/JustinChristopher2097/JustinChristopher2097.github.io)
