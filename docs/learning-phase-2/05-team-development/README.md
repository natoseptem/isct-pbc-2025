# Section 5: Team Development

## Overview

In this section, you'll learn how professional developers collaborate on code using Git and GitHub. These are essential skills for working on any real-world project.

## Learning Objectives

By the end of this section, you will:

- Understand why version control is essential
- Use VSCode's Git GUI (Source Control panel, sync button)
- Stage, commit, and push changes using VSCode
- Pull changes from GitHub to stay in sync
- Invite team members to collaborate on repositories
- Resolve merge conflicts using VSCode's conflict resolution UI
- Follow best practices for small team collaboration

## Why Learn This?

**Real-world scenarios:**

- 💼 **At work:** Teams of developers working on the same codebase
- 🚀 **Side projects:** Collaborating with friends remotely
- 📚 **Open source:** Contributing to projects used by millions
- 🏢 **Interviews:** Git skills are expected for developer positions

**Without version control:**

```
project_v1.zip
project_v2.zip
project_v2_final.zip
project_v2_final_ACTUAL.zip
project_v3_johns_edits.zip
project_FINAL_USE_THIS_ONE.zip
```

😰 Chaos!

**With version control:**

```
main branch (shared code)
↓
Pull → Work locally → Commit → Push
↓
Everyone stays in sync automatically
```

✅ Organized and professional!

## Our Workshop Approach

**Note:** In professional settings, teams use branches and pull requests for code review. However, for this 2-3 day workshop, we'll use a **simplified workflow**:

- **Main branch only** - Focus on fundamentals
- **VSCode GUI** - Visual, point-and-click operations
- **Direct collaboration** - Push and pull to stay in sync
- **Communication** - Coordinate to avoid conflicts

This approach lets you focus on building your product while learning Git essentials. You'll learn about branches and pull requests as reference knowledge!

## Section Structure

### [5.1 Version Control Basics (15 minutes)](01-version-control.md)
- What is version control?
- Why Git and GitHub?
- Core concepts: repository, commit, branch
- Real-world Git workflows (reference)
- Our simplified workshop approach

### [5.2 Working with VSCode Git (30 minutes)](02-vscode-git.md)
- VSCode Source Control panel
- Staging and committing with GUI
- Git Graph extension for visualizing history
- Viewing changes and diffs
- Hands-on: Make your first commits using VSCode

### [5.3 Collaborating with GitHub (30 minutes)](03-github-collaboration.md)
- Understanding local vs remote repositories
- Push and pull with VSCode sync button
- Inviting team members to repositories
- Team collaboration workflow
- Best practices for small teams
- Hands-on: Practice push-pull workflow with teammates

### [5.4 Handling Conflicts (15 minutes)](04-conflict-resolution.md)
- Why conflicts happen
- VSCode's conflict resolution UI
- Accept current/incoming/both changes
- Hands-on: Pair exercise creating and resolving conflicts
- Conflict prevention strategies

## Prerequisites

Before starting, ensure:

- [ ] Git is installed and configured (Section 3)
- [ ] GitHub account is created
- [ ] Project is pushed to GitHub
- [ ] You understand the code you've written (Section 4)

## Workflow You'll Learn

**Our simplified workflow using VSCode:**

```
1. Open VSCode and your project

2. Pull latest changes (click sync button)
   ↓ Gets teammates' changes

3. Make changes to code
   (Edit files in VSCode)

4. Open Source Control panel (Ctrl+Shift+G)
   ↓ See your changes

5. Stage changes (click + button)
   ↓ Select what to commit

6. Write commit message
   ↓ Describe your changes

7. Commit (click ✓ button or Ctrl+Enter)
   ↓ Save to local history

8. Push to GitHub (click sync button)
   ↓ Share with team

9. Repeat! Pull → Edit → Commit → Push
```

**All done with point-and-click in VSCode!**

## Key Concepts

### Repository (Repo)

A project tracked by Git:
- Contains all files and folders
- Stores complete history of changes
- Can be local (your computer) or remote (GitHub)

### Commit

A snapshot of your project at a point in time:
- Like a save point in a video game
- Has a unique ID (hash)
- Includes message describing changes
- Can revert to any commit

### Branch

An independent line of development:
- `main` - shared production code
- `feature/X` - working on new feature X (professional workflow)
- `bugfix/Y` - fixing bug Y (professional workflow)

**Note:** In this workshop, we'll work directly on the `main` branch to keep things simple. Branches are important for professional work, and you'll learn about them as reference knowledge in 5.1!

## Common Terms

| Term | Meaning |
|------|---------|
| **Clone** | Download a repository from GitHub to your computer |
| **Fork** | Create your own copy of someone else's repository |
| **Stage** | Mark files to be included in next commit |
| **Commit** | Save staged changes with a message |
| **Push** | Upload commits to remote repository (GitHub) |
| **Pull** | Download latest commits from remote |
| **Merge** | Combine changes from different branches |
| **Conflict** | When same code is changed differently in two branches |
| **HEAD** | Pointer to current branch/commit |
| **Origin** | Default name for remote repository |

## VSCode Git Operations Quick Reference

**In this workshop, you'll use VSCode's GUI instead of command-line Git:**

| Operation | VSCode Method |
|-----------|---------------|
| **Check status** | Open Source Control panel (Ctrl+Shift+G) |
| **Stage files** | Click + button next to file |
| **Stage all** | Click + button next to "Changes" header |
| **Unstage** | Click - button next to staged file |
| **Commit** | Type message, click ✓ or Ctrl+Enter |
| **Push** | Click sync button (bottom left) |
| **Pull** | Click sync button (bottom left) |
| **View changes** | Click on file in Changes list |
| **View history** | Use Git Graph extension |
| **Discard changes** | Right-click file → Discard Changes |

**No command line needed!** Everything is point-and-click.

## Git Commands Reference (Optional)

For reference, here are equivalent Git commands. **You don't need to use these** in this workshop, but they're helpful to know for future learning:

```bash
# Check status
git status

# Stage and commit
git add .
git commit -m "message"

# Push/Pull
git push
git pull

# View history
git log --oneline
```

**In professional work**, you might use either GUI or command line depending on preference. Both are equally valid!

## Tips for Success

### 1. Commit Often

```
❌ One commit at end of day with 100 changes
✅ Many small commits as you complete each piece
```

**Benefits:**
- Easier to review
- Easier to find bugs
- Can revert small changes
- Better documentation

### 2. Write Good Commit Messages

```
❌ "fixed stuff"
❌ "asdfasdf"
❌ "changes"

✅ "Add delete button to pet cards"
✅ "Fix age calculation for cats"
✅ "Update button styling to use shadcn/ui"
```

**Format:**
```
<type>: <short description>

<optional longer description>

<optional references>
```

**Types:**
- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation
- `style:` - Formatting, no code change
- `refactor:` - Code change that neither fixes nor adds feature
- `test:` - Adding tests
- `chore:` - Maintenance tasks

### 3. Pull Before Pushing

**The sync button does this automatically!**

When you click the sync button in VSCode:
1. Pulls latest changes from GitHub
2. Merges them with your local commits
3. Pushes your commits back to GitHub

If there's a conflict, VSCode will help you resolve it!

### 4. Don't Commit Secrets

**Never commit:**
- API keys
- Passwords
- Database credentials
- `.env.local` files

These should be in `.gitignore`!

### 5. Communicate with Your Team

**For this workshop:**
```
✅ Tell teammates which files you're editing
✅ Pull frequently to get their changes
✅ Push frequently to share your changes
✅ Coordinate before editing the same file

💬 "I'm working on PetCard.tsx"
💬 "I'll handle the homepage"
💬 "I just pushed my changes!"
```

**Note:** In professional work, teams use branches and pull requests to coordinate. We're simplifying for this workshop, but communication is even more important!

## Collaboration Workflows

### Our Workshop Workflow (Simplified)

```
main branch (everyone works here)
  ↓
Alice: Pull → Edit file A → Commit → Push
  ↓
Bob: Pull (gets Alice's changes) → Edit file B → Commit → Push
  ↓
Carol: Pull (gets both changes) → Edit file C → Commit → Push
  ↓
Everyone pulls to stay in sync
```

**Key practices:**
- Work on different files when possible
- Pull frequently (every 30-60 min)
- Push when done with a feature
- Communicate which files you're editing

### Professional Workflows (Reference)

**Small Team with Branches:**
```
main (protected)
  ├─ alice/feature-A → PR → Review → Merge
  ├─ bob/feature-B → PR → Review → Merge
  └─ carol/bugfix-C → PR → Review → Merge
```

**Large Team with Development Branch:**
```
main (production)
  ↓
develop (integration)
  ├─ feature-A
  ├─ feature-B
  └─ feature-C
```

These workflows use branches and pull requests for better code review and quality control. You'll learn about them in 5.1 as reference knowledge!

## What Could Go Wrong?

### Merge Conflicts

**When:** Two people edit the same line in the same file
**Solution:** VSCode's conflict resolution UI will help you choose which version to keep (you'll practice this in 5.4!)

### Authentication Issues

**When:** VSCode can't push to GitHub
**Solution:** Sign in to GitHub in VSCode (bottom left account icon)

### Pushed Secrets

**When:** Accidentally committed API keys or passwords
**Solution:** Rotate the keys immediately! Deleting the commit doesn't remove it from history.

**Prevention:**
- Check your `.gitignore` file
- Never commit `.env.local` files
- Review changes before committing

### Someone Can't Push

**When:** Teammate gets "permission denied" error
**Solution:** Make sure they're invited as a collaborator on GitHub (Settings → Collaborators)

## Ready to Start?

You're about to learn skills that professional developers use every single day. We'll use a simplified, VSCode-focused approach perfect for this workshop.

**Remember:**
- **VSCode does the heavy lifting** - everything is point-and-click
- **It's okay to make mistakes** - that's what version control is for!
- **You can always undo changes** - Git keeps your history safe
- **Communicate with your team** - coordinate to avoid conflicts
- **Ask for help if stuck** - we're all learning together!

**The simplified workflow you learn here teaches the fundamentals.** When you're ready for professional development, the concepts transfer directly to branch-based workflows!

**Let's begin with [5.1 Version Control Basics →](01-version-control.md)**

---

**Navigation:**
- **Previous:** [← Section 4: Programming Basics](../04-programming-basics/README.md)
- **Next:** [5.1 Version Control Basics →](01-version-control.md)
- **Home:** [README](../../README.md)
