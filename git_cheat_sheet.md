# Git & GitHub — Beginner Cheat Sheet

A practical reference for everyone working on this project. No prior git experience
needed. If anything here looks confusing or something seems to have gone wrong,
**stop and ask before continuing** — git rarely loses work, but guessing can make a
small problem bigger.

---

## 1. The mental model (learn these 4 words first)

| Word | What it means | Where it lives |
|---|---|---|
| **Repository (repo)** | A project folder that git is tracking | Your computer + GitHub |
| **Commit** | A saved snapshot of your files, with a short note on what changed | Your computer |
| **Push** | Upload your commits to GitHub so others can see them | → GitHub |
| **Pull** | Download other people's commits from GitHub to your computer | GitHub → you |

The whole daily rhythm is just: **pull** (get the latest) → make changes → **commit**
(snapshot) → **push** (share). That's 90% of git.

---

## 2. One-time setup (do this once per computer)

**a. Install the tools**
- **git** — on Ubuntu: `sudo apt install git`. On Windows/Mac: install from git-scm.com.
- **VS Code** — from code.visualstudio.com (optional but recommended for beginners).
- A **GitHub account** — sign up at github.com.

**b. Tell git who you are** (so your commits are labeled). In a terminal:
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

**c. Get the project onto your computer ("clone" it)**
Cloning = downloading a copy of the repo that stays linked to GitHub.
- **In VS Code:** open the Command Palette (Ctrl+Shift+P / Cmd+Shift+P) →
  type "Git: Clone" → paste the repo's GitHub URL → pick a folder. VS Code will
  prompt you to sign in to GitHub in your browser the first time.
- **In the terminal:**
  ```bash
  git clone <repo-url>
  cd <repo-folder>
  ```

> **Sign-in tip (terminal):** GitHub no longer accepts your password on the command
> line. The easiest fix is the GitHub CLI: install `gh` (`sudo apt install gh`), run
> `gh auth login` once, and pushing/pulling just works afterward.

---

## 3. The daily workflow

### The golden first step: PULL before you start
Always get everyone else's latest changes before you begin working, so you're not
editing an old version.
- **VS Code:** click the **Sync Changes** button (or the ↻ icon in the Source Control panel).
- **Terminal:** `git pull`

### Then: make your changes
Edit files, add new ones — work normally.

### Then: commit and push

**In VS Code (click-path):**
1. Open the **Source Control** panel (branching icon on the left, or Ctrl+Shift+G).
2. Your changed files appear under "Changes." Click **+** next to each one to **stage** it
   (mark it for the snapshot). Or click the + on "Changes" to stage all.
3. Type a short **commit message** in the box (e.g. `Add depth capture script`).
4. Click **✓ Commit**.
5. Click **Sync Changes** (or **Push**) to upload to GitHub.

**In the terminal:**
```bash
git pull                       # get latest first
git status                     # see what changed (safe — just shows info)
git add .                      # stage ALL changes (or: git add <filename>)
git commit -m "Short message"  # snapshot, with a message
git push                       # upload to GitHub
```

---

## 4. Working as a team (important)

Everyone shares one repo, so a little discipline keeps it smooth:

- **Pull before you start, every time.** This is the #1 way to avoid conflicts.
- **Commit small and often**, with clear messages. Ten small commits beat one giant one.
- **Push when you finish a chunk of work** so teammates get it.
- **Tell each other** when you're working on the same file at the same time.

**What's a "merge conflict"?** If two people change the *same lines* of the *same file*
and both push, git can't decide which wins, and asks a human to choose. It looks scary
(you'll see `<<<<<<<`, `=======`, `>>>>>>>` markers in the file) but nothing is lost.
If you hit one: **don't panic, don't guess — ask** whoever knows git, or save your work
elsewhere first. VS Code has a visual tool that makes resolving these much easier.

> **When you're ready to level up:** teams often use *branches* (each person works on
> their own copy of the code, then merges it in via a "pull request"). You don't need
> this to start — everyone working on the main branch with "pull first" is fine for a
> small team — but it's the natural next step once you're comfortable.

---

## 5. Golden rules (what keeps a repo healthy)

- ✅ **Write clear commit messages.** "Fix camera timeout bug" — not "stuff" or "update".
- ✅ **Pull before you push.** Avoids most conflicts.
- ✅ **Commit code and docs**, not giant data files. Big files (datasets, point-cloud
  recordings, build outputs) bloat the repo. Keep them out — ask about a `.gitignore`
  file, which tells git to ignore certain files/folders.
- ✅ **Never commit secrets** — passwords, API keys, private patient data. Once pushed,
  assume it's permanent.
- ⚠️ **If a command or message confuses you, stop and ask.** Especially anything
  mentioning `reset --hard`, `force push`, or `rebase` — those can discard work.

---

## 6. Quick command reference

| Task | Terminal command | VS Code |
|---|---|---|
| Copy the repo to your computer | `git clone <url>` | Palette → "Git: Clone" |
| See what changed | `git status` | Source Control panel |
| Get teammates' latest | `git pull` | Sync Changes / ↻ |
| Stage changes | `git add .` | **+** next to files |
| Save a snapshot | `git commit -m "message"` | ✓ Commit |
| Upload to GitHub | `git push` | Sync Changes / Push |
| See commit history | `git log --oneline` | Source Control → graph |

---

## 7. Mini-glossary

- **clone** — make a local copy of a GitHub repo (do this once).
- **stage** — mark which changes go into the next commit.
- **commit** — a saved snapshot + message.
- **push / pull** — upload to / download from GitHub.
- **branch** — a parallel line of work (advanced; optional at first).
- **merge conflict** — git needs a human to decide between two edits to the same lines.
- **.gitignore** — a file listing things git should NOT track (big data, build outputs, secrets).
- **remote** — the GitHub copy of the repo (called `origin` by default).

---

*Keep this file in the repo so new team members find it on day one.
When in doubt: pull, commit small, write a clear message, and ask before doing anything
that sounds destructive.*