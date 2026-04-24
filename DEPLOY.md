# Deploying The Book of Answers — Step by Step

This guide walks you through getting this web app live on the internet using **GitHub** (code storage + version control) and **Vercel** (free hosting). Both are free. You only need to do the setup steps once — after that, every future update is just a push.

---

## What You'll Need

- A GitHub account (you have one)
- A Vercel account (free — you'll create it below)
- Git installed on your Mac (it almost certainly already is — `git --version` in Terminal to check)

---

## Part 1 — Set Up Git on Your Mac (One-Time)

Open **Terminal** (Spotlight → type Terminal → Enter).

### 1.1 Check if Git is installed
```
git --version
```
You should see something like `git version 2.x.x`. If not, macOS will prompt you to install Xcode Command Line Tools — just follow that prompt.

### 1.2 Tell Git who you are (one-time, global setting)
```
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```
Use the same email as your GitHub account.

### 1.3 Set up GitHub authentication (one-time)
GitHub no longer accepts passwords over the command line. The easiest modern approach is the **GitHub CLI**:

1. Install it: go to https://cli.github.com and download the macOS installer
2. Run: `gh auth login`
3. Choose: **GitHub.com** → **HTTPS** → **Login with a web browser**
4. Follow the prompts — it will open a browser window to confirm

You're now authenticated. You won't need to enter credentials again.

---

## Part 2 — Create the GitHub Repository

### 2.1 Create a new repo on GitHub
1. Go to https://github.com/new
2. Repository name: `book-of-answers` (or whatever you like)
3. Description: `A web version of The Book of Answers`
4. Set it to **Public** (required for free Vercel hosting)
5. **Do NOT** check "Add a README file" — we already have files ready
6. Click **Create repository**

### 2.2 Initialize Git in your project folder
In Terminal, navigate to this folder:
```
cd ~/path/to/your/Projects/web/answers
```
(Replace the path with wherever your Projects folder actually lives on your Mac.)

Then run these commands one at a time:
```
git init
git add .
git commit -m "initial commit: book of answers web app"
```

### 2.3 Connect your local folder to GitHub and push
GitHub will show you these commands after you create the repo — they'll look like:
```
git remote add origin https://github.com/YOUR_USERNAME/book-of-answers.git
git branch -M main
git push -u origin main
```
Copy those exact commands from GitHub and run them in Terminal. After this, refresh your GitHub repo page — you should see your files.

---

## Part 3 — Deploy on Vercel

### 3.1 Create a Vercel account
1. Go to https://vercel.com
2. Click **Sign Up**
3. Choose **Continue with GitHub** — this links your accounts automatically

### 3.2 Import your GitHub repo
1. Once logged in, click **Add New → Project**
2. You'll see your GitHub repos listed — find `book-of-answers` and click **Import**
3. Vercel will auto-detect it as a static site (no framework needed)
4. Leave all settings as defaults
5. Click **Deploy**

Vercel will build and deploy in about 10–20 seconds. You'll get a live URL like:
```
https://book-of-answers-yourusername.vercel.app
```

That's it. Your app is live on the internet. 🎉

### 3.3 Optional: Set a custom domain
In your Vercel project settings → **Domains**, you can add any domain you own. Vercel handles the SSL certificate automatically.

---

## Part 4 — Making Updates (The Everyday Workflow)

This is the loop you'll use every time you change something:

```
# 1. Make your changes to any file in the project

# 2. Stage the changed files
git add .

# 3. Commit with a message describing what you did
git commit -m "describe what you changed"

# 4. Push to GitHub
git push
```

That's it. Vercel watches your GitHub repo — as soon as you push, it auto-redeploys. The live site updates in about 15 seconds.

---

## Understanding What You Just Built

Here's the mental model for this whole stack:

```
Your computer  →  GitHub  →  Vercel  →  Internet
  (source)       (backup +    (hosting)   (users)
                  history)
```

- **Git** is the tool that tracks changes and packages your files
- **GitHub** is where your code lives in the cloud (also your version history)
- **Vercel** watches GitHub and serves your files to anyone in the world

This is a **static site** — meaning there's no server, no database, no backend. It's just HTML, CSS, JS, and some images. Vercel hosts it for free on a global CDN (Content Delivery Network), which means it loads fast everywhere.

---

## Project File Structure

```
answers/
├── index.html        ← the entire app lives here
├── OpenEye-01.png    ← eye closed
├── OpenEye-02.png    ← eye half open
├── OpenEye-03.png    ← eye open (answer revealed)
├── .gitignore        ← tells Git what NOT to track
└── DEPLOY.md         ← this file
```

---

## Troubleshooting

**`git push` asks for a password and fails**
→ Make sure you completed Part 1.3 (GitHub CLI auth). Run `gh auth login` again.

**Vercel says "no framework detected"**
→ That's fine! Just leave Framework Preset as "Other" and deploy. Static HTML works perfectly.

**Images not showing on the live site**
→ File names are case-sensitive on servers. Make sure `OpenEye-01.png` in your HTML matches exactly (capital O, capital E).

**Changes aren't showing on the live site**
→ Check that you ran `git push` (not just `git commit`). Also try a hard refresh in the browser: Cmd + Shift + R.
