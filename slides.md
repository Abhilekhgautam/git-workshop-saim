---
theme: gaia
_class: lead
paginate: true
backgroundColor: #ffffff
style: |
  section {
    font-size: 30px;
  }
  h1 {
    color: #2b3137;
  }
  code {
    background: #f6f8fa;
    color: #e36209;
  }
  .box {
    padding: 10px;
    background: #e1e4e8;
    border-radius: 5px;
  }
---

# 🐙 Git & GitHub
## From Solo Coder to Collaborative Team

Hands-on Workshop

---

# 👨‍💻 About Me

* **Abhilekh Gautam**
* **C++ Systems Engineer** @ GuardWare Australia 
* **Technical Writer**
* **Independent Researcher** in Programming Languages and Compilers

---

# ⚠️ Rule #1 for Today

**This is not a lecture.** 

We will break things. 
We will create conflicts. 
Code will "disappear."
*And we will learn how to fix all of it.*

Please interrupt me if you get stuck!

---

# 🎯 Workshop Goals

By the end of this session, you will:

1. Understand the Git mental model 
2. Setup and use GitHub as a team
3. Open, review, and merge Pull Requests (PRs)
4. Defeat the final boss: **Merge Conflicts**
5. Simulate a team sprint
6. Automate tasks using GitHub Actions

---

# 📁 Why Git Exists

Before Git, how did we save different versions of code? 
We used the **"Zip Folder Method"**:

    engine_final.zip
    engine_final_v2.zip
    engine_FINAL_final_USE_THIS.zip
    engine_Sagar_edit_DONT_DELETE.zip

**The Problems:**
* Which one is *actually* the latest?
* What exact C++ code changed between v2 and v3?
* How do Sagar and Samir combine their zip files without deleting each other's work?

---

# 🥊 Git vs. GitHub

They are **not** the same thing! 

**Git:**
* The core engine / software.
* Runs locally on your computer. Works perfectly offline.
* Tracks the history and changes of your files.

**GitHub:**
* A website (owned by Microsoft) that hosts Git repos in the cloud.
* Gives us a UI for teamwork (Pull Requests, Issue tracking).
* *Analogy: Git is the video file, GitHub is YouTube.*

---
# GitLab
 
* Gitlab, Open Source alternative to Github.

---
# 🛠️ Step 0: The Absolute Basics

Before we do anything, Git needs to know who you are.
Open your terminal and type:

    git config --global user.name "Your Real Name"
    git config --global user.email "your.email@example.com"

*Verify it worked:*

    git config --list

---

<!-- _class: lead -->
# Part 1: Solo Survival Mode
*(Local Git)*

---

# 🧠 The Mental Model

Git becomes easy when you stop memorizing commands and understand the **4 areas**:

      Edit              Add               Commit            Push
     ┌────────┐      ┌─────────┐       ┌─────────┐       ┌─────────┐
     │WORKING │ ────►│STAGING  │ ─────►│  LOCAL  │ ────► │ REMOTE  │
     │  DIR   │      │  AREA   │       │   REPO  │       │  REPO   │
     └────────┘      └─────────┘       └─────────┘       └─────────┘
          ▲               │                 │                 │
          │               │                 │                 │
          └───────────────┴──── Pull / Merge ─────────────────┘

---

# ⌨️ Hands-on #1: The Basics

Let's create history. Run these commands:

    mkdir workshop-solo
    cd workshop-solo
    git init

Create a file:

    echo "# My Project" > README.md
    git status

*Notice it's red! It's in the Working Directory.*

---

# ⌨️ Hands-on #1: The Commit

Move it to the Staging Area:

    git add README.md
    git status

*Notice it's green! It's ready to be saved.*

Save it to the Local Repo:

    git commit -m "Initial commit: Add README"
    git log

---

# 🕰️ Hands-on #2: Time Travel

Git never loses code (mostly). Let's prove it.

1. Edit your README.md. Add a new line: "This is a terrible mistake."
2. Save the file.
3. Check git status.

Wait, we didn't mean to do that! How do we undo?

    git restore README.md

*Look at the file again. The mistake is gone!*

---

<!-- _class: lead -->
# Part 2: Multi-Player Mode
*(GitHub & Collaboration)*

---

# 🌿 Branches

A branch is simply an isolated timeline.

    main
     A --- B --- C

Create a branch: git switch -c feature-login

    main
     A --- B --- C
                  \
    feature-login  \
                    D --- E

*You can break everything on feature-login and main stays safe.*

---

# 🔄 The Industry Standard Workflow

1. Create Issue (What are we building/fixing?)
2. Create Branch (git switch -c ticket-123)
3. Write Code & Commit
4. Push to GitHub
5. **Open Pull Request (PR)**
6. Team Review 
7. Merge to main

---

<!-- _class: lead -->
# 🤝 Hands-on #3: Pair Programming
*(Find a partner!)*

---

# 🎭 Scenario 1: The Code Review

**Decide who is Developer A and Developer B.**

**Developer A:**
1. Create a new repo on GitHub (Public).
2. Add a basic index.html file, commit, and push.
3. Go to Repo Settings -> Collaborators -> Add Developer B.

**Developer B:**
1. Accept the invite.
2. Clone the repo to your computer.

---

# 🎭 Scenario 1: The Pull Request

**Developer B:**
1. Create branch: git switch -c add-styling
2. Add some CSS to index.html.
3. Add and commit: git commit -am "Add cool CSS"
4. Push branch: git push -u origin add-styling
5. Go to GitHub and open a **Pull Request**.

**Developer A:**
1. Go to the PR on GitHub.
2. Leave a comment requesting a change.

---

# 🎭 Scenario 1: Resolving Feedback

**Developer B:**
1. Make the requested change locally.
2. Commit again: git commit -am "Update background to blue"
3. Push: git push
*(Notice the PR updates automatically!)*

**Developer A:**
1. Approve the PR.
2. Click **Squash and Merge**.

*🎉 Congratulations! You just completed a professional code cycle.*

---

<!-- _class: lead -->
# Part 3: When Things Go Wrong
*(Merge Conflicts)*

---

# ⚔️ What is a Merge Conflict?

A conflict is **not an error**. 
It is Git saying: *"I am a robot. You both changed the exact same line of code. I need a human to tell me which one to keep."*

    <<<<<<< HEAD (Your local code)
    int count = 10;
    =======
    int count = 20;
    >>>>>>> feature-branch (Incoming code)

---

<!-- _class: lead -->
# 🥊 Hands-on #4: The Conflict Simulator
*(Stay with your partner)*

---

# 🥊 Step 1: Create the Setup

Both **Dev A** and **Dev B**:
Run git checkout main and git pull so you are perfectly synced.

**Dev A:**
Change line 1 of index.html to: Title A.
Commit and push to main.

**Dev B:**
Change line 1 of index.html to: Title B.
Commit... and try to push to main.

---

# 🥊 Step 2: The Block

**Dev B, your push was rejected.**
Git will tell you to pull first.

**Dev B:** Run git pull
**BOOM.** Merge Conflict.

Open the file in your code editor. You will see the marker arrows.

---

# 🥊 Step 3: The Resolution

**Dev B:**
1. Delete the Git markers.
2. Keep the code you actually want.
3. Save the file.
4. git add index.html
5. git commit -m "Resolve merge conflict"
6. git push

*You have defeated the monster.*

---

<!-- _class: lead -->
# Part 4: The Final Boss
*(Group Sprint Simulation)*

---

# 🏢 Group Exercise: "The Recipe App"

**Form groups of 3 (or 4).**
*Assign Roles: Lead Dev, UI Dev, Backend Dev.*

**Lead Dev:** 
1. Create a GitHub repo called recipe-app.
2. Add Collaborators.
3. Create a recipe.txt file with ONE line: My Recipe App. Push to main.

*Everyone: Clone the repo.*

---

# 🏢 The Sprint Starts Now

**DO NOT COMMUNICATE UNTIL YOU HIT A CONFLICT.**

*   **UI Dev:** Create branch ui-update. Add HTML tags around the text in recipe.txt. Push and open PR.
*   **Backend Dev:** Create branch add-ingredients. Add 3 ingredients to recipe.txt. Push and open PR.
*   **Lead Dev:** Create branch add-instructions. Add 3 cooking steps to recipe.txt. Push and open PR.

---

# 🏢 Code Review & Merge Chaos

1. Everyone must review someone else's PR and leave at least one comment.
2. The **Lead Dev** merges the first PR.
3. The next person tries to merge their PR... **CONFLICT!**
4. You must pull main into your local branch, resolve the conflict, push again, and *then* merge the PR.

*Goal: Get all 3 features merged into main cleanly.*

---

<!-- _class: lead -->
# Part 5: Automation
*(Intro to GitHub Actions)*

---

# 🤖 What are GitHub Actions?

Tired of doing chores manually?
GitHub Actions are cloud robots that run tasks automatically when things happen in your repo.

**Common uses:**
* Run automated C++ compilation/tests on every PR (CI)
* Check code formatting
* Deploy builds automatically (CD)
* Send a message to Slack on a new release

---

# 📝 The Workflow File

Workflows live inside a special hidden folder:
.github/workflows/

They are written in **YAML** (a simple configuration language).

They consist of two main parts:
1. **Triggers:** When should the robot wake up? (e.g., on push)
2. **Jobs:** What should the robot do? (e.g., run tests)

---

# ⚙️ Example: "Say Hello" Action

Create a file at .github/workflows/hello.yml:

    name: Hello World Action
    
    on: [push]
    
    jobs:
      say-hello:
        runs-on: ubuntu-latest
        steps:
          - name: Print a message
            run: echo "Someone pushed code! The robot is awake!"

---

# 🧪 Hands-on #5: Your First Action

**Stay in your Recipe App groups!**

1. Create a folder named exactly: .github
2. Inside it, create a folder named exactly: workflows
3. Inside that, create: test.yml
4. Paste the code from the previous slide.
5. Commit and Push to main.
6. Open your repo on GitHub, and click the **Actions** tab at the top.

*Watch the robot execute your code in the cloud!*

---

# 🚑 Oh No, I Messed Up! (Cheat Sheet)

**"I staged files I didn't want to!"**
git restore --staged filename

**"My last commit message has a typo!"**
git commit --amend -m "Correct message"

**"I want to throw away all my uncommitted changes!"**
git restore . (Warning: Cannot be undone!)

**"I pushed a broken commit to main!"**
git revert commit-hash (Creates a reverse commit safely)

---

# 🔀 Merge vs Rebase

One of the most common interview questions!

**Merge:** Combines histories. "Let's join these two timelines." (Creates a merge commit).
**Rebase:** Rewrites history. "Let me pretend I started my work *after* the latest changes on main." (Creates a straight, linear line).

**Golden Rule:** NEVER rebase a branch that other people are using. Only rebase your own local, unpushed branches.

---

# 🌟 GitHub Pro-Tips

1. **Closing Issues:** If you name your PR "Fixes #4", GitHub automatically closes Issue #4 when the PR merges.
2. **.gitignore:** Create this file to tell Git to ignore files. (Never commit passwords!).
3. **Blame:** Use git blame filename to see exactly who wrote a specific line of code (and when). 

---

# 🎓 Key Takeaways

* **Commit often.** 
* **Never work directly on main.** Always branch.
* **Pull before you push.**
* **Review code nicely.** Suggest, don't demand.
* **Automate chores** with GitHub actions.
* **Don't panic on conflicts.** Read the markers, choose the code, commit.

---

<!-- _class: lead -->
# 🚀 Thank You!
Questions? 

Let's build awesome things together.
