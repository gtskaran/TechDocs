Git Infographic Study Notes (Beginner → Professional)
1. What is Git?
Developer
    │
    ▼
+----------------+
|      Git       |
| Version Control|
+----------------+
    │
    ├── Stores history
    ├── Tracks changes
    ├── Enables teamwork
    └── Allows rollback

Definition

Git is a Distributed Version Control System (DVCS) used to track source code changes, collaborate with teams, and maintain project history.

Benefits

✅ Track every change

✅ Restore old versions

✅ Team collaboration

✅ Safe experimentation

✅ Branch and merge features

2. History of Git
2002
 │
 ▼
Linux Kernel uses BitKeeper
 │
 ▼
2005
BitKeeper license issues
 │
 ▼
Linus Torvalds creates Git
 │
 ▼
2005+
Open Source Adoption
 │
 ▼
Today
Most Popular VCS

Created By

👨‍💻 Linus Torvalds (Creator of Linux)

Goals
Fast
Distributed
Secure
Reliable
Open Source
3. Why Git is Needed?
Without Git
project_final.zip
project_final_v2.zip
project_final_latest.zip
project_final_latest_fixed.zip
project_final_final.zip


Problems:

❌ Confusing versions

❌ No change history

❌ Difficult collaboration

❌ Accidental overwrites

With Git
Project
 │
 ├── Commit 1
 ├── Commit 2
 ├── Commit 3
 └── Commit 4


Benefits:

✅ Complete history

✅ Compare changes

✅ Multiple developers

✅ Easy rollback

✅ Backup via GitHub/GitLab

4. Git Architecture
Working Directory
       │
       ▼
     git add
       │
       ▼
Staging Area
       │
       ▼
   git commit
       │
       ▼
 Local Repository
       │
       ▼
    git push
       │
       ▼
 Remote Repository

5. Git Installation & Setup
Install Git
Windows

https://git-scm.com/downloads

Verify
git --version


Example:

git version 2.x.x

Configure Git
git config --global user.name "Your Name"
git config --global user.email "your@email.com"


Check Configuration:

git config --list

6. Create a New Project Repository
Step 1

Create Project

MyProject
 ├── index.html
 ├── app.js
 └── style.css

Step 2

Initialize Git

git init


Output:

Initialized empty Git repository

7. Git Basic Workflow
Create File
    │
    ▼
git add
    │
    ▼
git commit
    │
    ▼
git push

Check Status
git status


Shows:

Modified files
New files
Deleted files
Add Single File
git add app.js

Add All Files
git add .

Commit
git commit -m "Initial commit"


Example:

git commit -m "Added login page"

View History
git log


Compact:

git log --oneline

8. Understanding Git Ignore
Why .gitignore?

Prevent unnecessary files from entering repository.

Examples:

node_modules
logs
temp files
IDE settings

Create .gitignore
node_modules/
.env
*.log
*.tmp

Example Structure
Project
 │
 ├── .gitignore
 ├── src
 ├── package.json
 └── README.md


Ignored files won't be committed.

9. Git Branching Basics
main
 │
 ├── feature-login
 │
 └── feature-payment

Create Branch
git branch feature-login

Switch Branch
git checkout feature-login


or

git switch feature-login

Create + Switch
git checkout -b feature-login

List Branches
git branch

10. Merging Branches
main
 │
 └── feature-login
          │
       merge
          ▼
        main


Merge:

git checkout main
git merge feature-login

11. GitHub vs GitLab
Feature	GitHub	GitLabPopularity	Very High	High
Open Source Projects	Excellent	Good
CI/CD	Good	Excellent
Self Hosting	Limited	Strong
Community	Huge	Large
Git
 │
 ├── GitHub
 └── GitLab

Remember

Git = Tool

GitHub/GitLab = Cloud Hosting Platforms

12. Connect Git to GitHub
Create Repository on GitHub

Example:

https://github.com/user/MyProject

Add Remote
git remote add origin https://github.com/user/MyProject.git


Verify:

git remote -v

13. First Push to GitHub
git add .
git commit -m "Initial commit"
git branch -M main
git push -u origin main


Flow:

Local PC
   │
   ▼
Git
   │
   ▼
GitHub Repository

14. Clone Existing Repository
git clone https://github.com/user/project.git


Creates:

project
 ├── src
 ├── docs
 └── README.md

15. Daily Git Workflow
Pull
 │
 ▼
Code
 │
 ▼
Add
 │
 ▼
Commit
 │
 ▼
Push


Commands:

git pull origin main

git add .

git commit -m "Completed feature"

git push origin main

16. Using Git with VS Code
Open Folder
File
 └── Open Folder

Source Control Panel
VS Code
 └── Source Control
     ├── Changes
     ├── Commit
     ├── Push
     └── Pull


Shortcut:

Ctrl + Shift + G

Initialize Repository

Source Control → Initialize Repository

Equivalent:

git init

Commit from VS Code
Changes
   │
   ▼
Message
   │
   ▼
Commit

Sync Changes
GitHub
 ▲     ▼
Pull  Push


Click:

Sync Changes


VS Code automatically handles:

git pull
git push

17. Connect VS Code to GitHub
Method 1

Account Icon → Sign In

VS Code
    │
    ▼
GitHub Account

Method 2

Install Extension:

GitHub Pull Requests and Issues


Workflow:

VS Code
   │
   ▼
Git
   │
   ▼
GitHub

18. Git Desktop (GitHub Desktop)
What is GitHub Desktop?

GUI tool for Git operations.

No command line needed.

Workflow
Repository
     │
     ▼
 Make Changes
     │
     ▼
 Commit
     │
     ▼
 Push Origin

Typical Steps
Clone Repository
File
 └── Clone Repository

Commit
Changes
 └── Commit to Main

Push
Push Origin

Pull
Fetch Origin

19. Complete Git Workflow Infographic
Create Project
      │
      ▼
git init
      │
      ▼
git add .
      │
      ▼
git commit
      │
      ▼
Connect GitHub
      │
      ▼
git remote add origin URL
      │
      ▼
git push
      │
      ▼
GitHub Repository
      │
      ▼
Team Collaboration
      │
      ▼
git pull
      │
      ▼
Continue Development

20. Most Used Git Commands Cheat Sheet
git init
git clone URL

git status

git add .
git add filename

git commit -m "message"

git log --oneline

git branch
git branch feature

git checkout feature
git checkout -b feature

git merge feature

git pull origin main

git push origin main

git remote -v

git remote add origin URL

git fetch

git stash

git reset

git revert

Golden Rule
Code
  ↓
git add .
  ↓
git commit -m "Meaningful Message"
  ↓
git pull
  ↓
git push


This sequence covers the entire Git journey: History → Need → Installation → Git Basics → .gitignore → VS Code → GitHub/GitLab → Syncing → GitHub Desktop → Daily Workflow.



Visual Infographic Layout: Git Complete Learning Roadmap
Canvas Size

1080 × 5000 px (Vertical Infographic)

Color Theme
Git Orange: #F05033
GitHub Black: #181717
GitLab Orange: #FC6D26
VS Code Blue: #007ACC
Background: #F5F7FA
Text: Dark Gray #2D3748
HEADER SECTION
┌─────────────────────────────────┐
│                                 │
│           GIT ROADMAP           │
│                                 │
│     Beginner → Professional     │
│                                 │
└─────────────────────────────────┘


Visual:

      💻
       │
       ▼
      GIT
       │
 ┌─────┼─────┐
 ▼     ▼     ▼
GitHub GitLab VSCode

SECTION 1
WHAT IS GIT?
┌─────────────────────────────┐
│          WHAT IS GIT        │
├─────────────────────────────┤
│ Version Control System      │
│ Tracks code changes         │
│ Maintains history           │
│ Enables collaboration       │
└─────────────────────────────┘


Visual Circle Diagram

        Git
         ●
    ╱    │    ╲
History Team Backup
         │
       Restore


Icons:

🕒 History

👨‍💻 Team

☁ Backup

↩ Restore

SECTION 2
HISTORY OF GIT

Horizontal Timeline

2002
 │
BitKeeper
 │
 ▼
2005
Linus Torvalds
creates Git
 │
 ▼
2010
GitHub Growth
 │
 ▼
Today
Industry Standard


Visual

────────●────────●────────●────────●
 2002     2005      2010      Today

SECTION 3
WHY GIT IS NEEDED?

Split Comparison Layout

WITHOUT GIT
❌ project_final.zip
❌ project_final_v2.zip
❌ project_final_latest.zip
❌ project_final_final.zip


Problems

Lost work
Version confusion
Overwrite mistakes

WITH GIT
Commit 1
   │
Commit 2
   │
Commit 3
   │
Commit 4


Benefits

✔ History
✔ Rollback
✔ Collaboration
✔ Backup

SECTION 4
GIT ARCHITECTURE

Large Flow Diagram

┌───────────────┐
│ Working Area  │
└──────┬────────┘
       │ git add
       ▼
┌───────────────┐
│ Staging Area  │
└──────┬────────┘
       │ commit
       ▼
┌───────────────┐
│ Local Repo    │
└──────┬────────┘
       │ push
       ▼
┌───────────────┐
│ Remote Repo   │
└───────────────┘


Use arrows in Git orange.

SECTION 5
INSTALL & CONFIGURE GIT

Visual Terminal Style

git --version

git config --global user.name "John"
git config --global user.email "john@email.com"


Flow

Download
    ↓
Install
    ↓
Configure
    ↓
Ready

SECTION 6
FIRST PROJECT

Folder Illustration

📁 MyProject
 ├── index.html
 ├── style.css
 └── app.js


Commands

git init
git add .
git commit -m "Initial commit"


Visual Flow:

Folder
  ↓
git init
  ↓
Repository Created

SECTION 7
DAILY GIT WORKFLOW

Centerpiece Graphic

 CODE
   │
   ▼
git add .
   │
   ▼
 git commit
   │
   ▼
 git push


Circular Process

Pull
 ↓
Code
 ↓
Add
 ↓
Commit
 ↓
Push
 ↓
Pull

SECTION 8
GITIGNORE

Visual Folder

Project
 ├── src
 ├── .gitignore
 └── README.md


Example

node_modules/
.env
*.log
dist/


Visual

✅ Commit
src/

✅ Commit
README.md

❌ Ignore
node_modules

❌ Ignore
.env

SECTION 9
BRANCHING

Tree Style Graphic

           main
             │
      ┌──────┴─────┐
      │            │
feature-A    feature-B


Command Box

git branch feature-A
git switch feature-A

SECTION 10
MERGING

Before

main
 │
 └── feature-login


After

main
 │
 ├── Login
 │
 ├── Dashboard
 │
 └── Payment


Visual Merge Arrow

Branch
   ╲
    ╲
     ├── Merge
    ╱
main

SECTION 11
GITHUB vs GITLAB

Two Column Card Design

┌─────────────┐
│   GitHub    │
├─────────────┤
│ Huge Community
│ Open Source
│ Easy UI
└─────────────┘

┌─────────────┐
│   GitLab    │
├─────────────┤
│ Strong CI/CD
│ Self Hosting
│ DevOps Tools
└─────────────┘


Below:

Git = Engine
GitHub/GitLab = Garage

SECTION 12
CONNECT TO GITHUB

Visual Flow

Local Project
      │
      ▼
git remote add
      │
      ▼
GitHub Repo


Commands

git remote add origin URL
git branch -M main
git push -u origin main

SECTION 13
CLONE EXISTING PROJECT

Illustration

GitHub Repo
      │
      ▼
 git clone URL
      │
      ▼
 Local Project


Command Box

git clone https://github.com/user/project.git

SECTION 14
USING GIT WITH VS CODE

Visual

┌───────────────┐
│   VS CODE     │
└───────┬───────┘
        │
        ▼
 Source Control
        │
 ┌──────┼──────┐
 ▼      ▼      ▼
Add   Commit  Push


Shortcut

CTRL + SHIFT + G

SECTION 15
GITHUB DESKTOP

Large GUI Mockup

 GitHub Desktop
 ┌─────────────────┐
 │ Changed Files   │
 │ Commit Message  │
 │ Commit Button   │
 │ Push Origin     │
 └─────────────────┘


Workflow

Edit
 ↓
Commit
 ↓
Push
 ↓
GitHub

FINAL SECTION
GIT COMMAND CHEAT SHEET

Grid Layout

git init
git clone

git add .
git status

git commit -m

git push
git pull

git branch
git merge

git fetch
git stash
git revert

FOOTER
Golden Git Flow
Create Project
      ↓
git init
      ↓
git add .
      ↓
git commit
      ↓
git push
      ↓
GitHub
      ↓
Team Collaboration
      ↓
git pull
      ↓
Continue Development

Bottom Banner
"Track Everything • Collaborate Anywhere • Deploy With Confidence"


This layout works well for Canva, PowerPoint, Figma, Visio, Draw.io, Illustrator, or a single-page training poster and fits a complete Git training session from beginner to advanced level.


