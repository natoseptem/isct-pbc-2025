# 5.1 Version Control Basics

## Objectives

- Understand what version control is and why it matters
- Learn about Git and GitHub
- Understand core concepts: repositories, commits, branches

## What is Version Control?

**Version control** (also called source control) is a system that tracks changes to files over time.

### The Problem Without Version Control

Imagine you're writing a research paper:

```
essay.docx
essay_v2.docx
essay_v2_final.docx
essay_v2_final_REAL.docx
essay_v3_with_johns_edits.docx
essay_SUBMIT_THIS_ONE.docx
```

**Problems:**
- 😰 Which file is the latest?
- ❓ What changed between versions?
- 🤔 Who made which changes?
- 😱 How to merge John's edits with yours?
- 💾 Takes up lots of storage space
- 🔙 Hard to undo specific changes

### The Solution: Version Control

With version control:

```
essay.docx (single file)
  ↓
Version history:
- v1: Initial draft (Nov 1, You)
- v2: Added introduction (Nov 3, You)
- v3: Fixed typos (Nov 5, John)
- v4: Added conclusion (Nov 6, You)
```

**Benefits:**
- ✅ One file, complete history
- ✅ See exactly what changed
- ✅ Know who made each change
- ✅ Revert to any previous version
- ✅ Merge changes from multiple people
- ✅ Work offline, sync later

## Why Software Needs Version Control

Software development has unique challenges:

### Multiple Developers

```
Taro is fixing a bug in UserAuth.ts
Hanako is adding a feature in UserAuth.ts
Jiro is refactoring UserAuth.ts

How do they all work without overwriting each other?
```

**Version control solves this!**

### Complex Changes

```
Project with 1,000 files
Change affects 50 files
Need to ensure all changes work together
Need to test before deploying
```

**Version control tracks everything!**

### History and Accountability

```
Bug introduced 3 weeks ago
Which change caused it?
Who wrote that code?
What was the reason?
```

**Version control provides answers!**

### Experimentation

```
Want to try a risky refactor
But don't want to break working code
Need ability to easily revert
```

**Version control enables safe experimentation!**

## Git: The Version Control System

**Git** is the most popular version control system in the world.

### History

- Created by Linus Torvalds in 2005
- Originally for Linux kernel development
- Now used by millions of developers
- Industry standard

### Why Git?

- **Distributed:** Every developer has full history
- **Fast:** Most operations are local
- **Branching:** Easy to create and merge branches
- **Popular:** Huge ecosystem and community
- **Free and open source**

## GitHub: Git Hosting Platform

**GitHub** hosts Git repositories in the cloud.

### What GitHub Provides

- **Remote storage:** Backup your code
- **Collaboration:** Share code with team
- **Pull requests:** Code review workflow
- **Issues:** Track bugs and features
- **Actions:** Automation (CI/CD)
- **Pages:** Host static websites
- **Discussions:** Community forums
- **Security:** Vulnerability scanning 
- and more

### Git vs GitHub

```
Git = The tool (version control software)
GitHub = The service (hosts Git repositories)
```

**Analogy:**
- Git = Email protocol
- GitHub = Gmail/Outlook

**Alternatives to GitHub:**
- GitLab
- Bitbucket
- Gitea (self-hosted)

But GitHub is the most popular (100+ million users).

## Core Concepts

### Repository (Repo)

A project tracked by Git.

```
my-project/
  .git/              ← Git stores history here
  src/
  README.md
  package.json
```

**Types:**
- **Local repo:** On your computer
- **Remote repo:** On GitHub

### Commit

A snapshot of your project at a point in time.

```
Commit: a3f5b2c
Author: You <you@example.com>
Date: Nov 6, 2024
Message: Add delete button to pet cards

Changes:
  components/PetCard.tsx    | +15 -2
  app/page.tsx             | +8 -0
```

**Each commit:**
- Has unique ID (hash): `a3f5b2c...`
- Contains all file changes
- Has author and timestamp
- Has descriptive message

**Commits are permanent** - history is never lost!

### Branch

An independent line of development.

```
main      A---B---C---F---G
                   \
feature            D---E
```

- **main:** Production-ready code
- **feature:** Work in progress

**Benefits:**
- Work on multiple features simultaneously
- Don't break working code
- Easy to experiment
- Organized collaboration

### Working Directory, Staging Area, Repository

Git has three areas:

```
Working Directory → Staging Area → Local Repository → Remote Repository
     (edit)           (git add)      (git commit)       (git push)
```

1. **Working Directory:** Your files, as you see them
2. **Staging Area:** Files marked for next commit
3. **Local Repository:** Committed history on your computer
4. **Remote Repository:** History on GitHub

## The Git Workflow

### Basic Cycle

```
1. Edit files
   ↓
2. Stage changes (git add)
   ↓
3. Commit changes (git commit)
   ↓
4. Push to GitHub (git push)
```

## Real-World Git Workflow (Reference)

In professional software development, teams use more sophisticated workflows for safety and quality:

### Branch-Based Development

```
main      A---B---C---F---G
                   \
feature            D---E
```

```
main branch (always working)
    ↓
feature branch (your work)
    ↓
Pull Request (review)
    ↓
Merge to main
```

**How it works:**
1. Create a branch for each feature/fix
2. Work on your branch without affecting main
3. When done, open a Pull Request (PR)
4. Team reviews your code
5. After approval, merge to main

**Benefits:**
- Main branch always works
- Safe experimentation on branches
- Code review catches bugs
- Clear history of what was added when

### Our Workshop Workflow

**We'll use a simplified approach:**

```
main branch only
    ↓
Everyone works on main
    ↓
Commit → Push → Pull
    ↓
Communicate about changes
```

**Why this works for our workshop:**
- ✅ Faster to learn
- ✅ Fewer tools to master
- ✅ Direct collaboration
- ✅ Focus on building product
- ✅ Still learn Git fundamentals

**Important:** This simplified workflow is **perfect for:**
- Learning Git basics
- Small teams (2-4 people)
- Short projects (hackathons, workshops)
- Rapid prototyping

**But in real jobs, you'll use:**
- Branch-based workflow
- Pull Requests
- Code reviews
- More safety measures

**Remember:** You're learning the fundamentals now. The advanced workflows build on these basics!

## Key Takeaways

- ✅ Version control tracks all changes to your code
- ✅ Git is the standard version control system
- ✅ GitHub hosts Git repositories and enables collaboration
- ✅ Commits are snapshots with messages
- ✅ Branches enable parallel development (we'll learn the simple workflow first)
- ✅ Professional teams use branches and Pull Requests (we'll use main branch only)
- ✅ Our simplified workflow is perfect for learning and small teams

## Common Questions

**Q: Do I need Git for small projects?**
A: Yes! Even solo projects benefit from version control. It's free backup, history, and experimentation.

**Q: How often should I commit?**
A: Frequently! Whenever you complete a logical unit of work (fix a bug, add a feature, refactor a function).

**Q: What if two people edit the same file?**
A: Git usually merges automatically. If it can't, you resolve conflicts manually (we'll practice this!).

**Q: Is my code public on GitHub?**
A: Only if you make the repository public. You can have private repositories (free on GitHub).

## What's Next?

Now that you understand *why* version control matters and *what* Git is, you're ready to use it!

In the next section, you'll learn how to use Git through **VSCode's graphical interface** - no command line required! You'll practice staging changes, committing, and viewing history, all with point-and-click.

---

**Navigation:**
- **Previous:** [← Section 5: Team Development](README.md)
- **Next:** [5.2 Working with VSCode Git →](02-vscode-git.md)
- **Home:** [README](../../README.md)
