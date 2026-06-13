# Crebrl AI Website — Setup, Hosting & Email Guide

This guide walks you through everything, end to end, assuming **zero prior
experience**. Total cost: **₹0** for hosting (free tier), and roughly
**₹450–₹500/month** for professional email if you choose Google Workspace
(or **free** if you choose the Cloudflare alternative described in Part 3).

---

## What you have

A folder called `crebrl-website` containing:

```
crebrl-website/
├── index.html       (Landing page)
├── products.html    (Products & Services page)
├── contact.html      (Contact page)
├── styles.css        (All design/styling)
├── script.js         (Mobile menu + contact form logic)
└── images/
    └── CrebrlAI_Logo.png
```

This is a **static website** — no database, no server code. This makes it
simple and free to host.

---

## Part 1 — Preview the site (optional, on your computer)

1. Download the `crebrl-website` folder/zip to your computer and unzip it.
2. Double-click `index.html` — it opens in your browser. You can click
   through to the other pages from the navigation menu.
3. The contact form **will not send messages yet** — that needs Part 2
   below.

---

## Part 2 — Set up the contact form (Formspree)

The contact form needs somewhere to send messages, since this is a static
site with no backend.

1. Go to **formspree.io** and click **Sign Up**. Use **hello@crebrl.ai**
   (or your personal email for now — you can change it later).
2. After verifying your email, click **New Form**. Name it "Crebrl AI
   Contact Form."
3. Formspree gives you an endpoint URL that looks like:
   `https://formspree.io/f/abcd1234`
4. Open `contact.html` in a text editor (Notepad, VS Code, etc.). Find this
   line near the form:
   ```html
   <form id="contactForm" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```
5. Replace `YOUR_FORM_ID` with the ID Formspree gave you (e.g. `abcd1234`).
6. Save the file. The free Formspree plan allows 50 submissions/month,
   which is more than enough to start.

---

## Part 3 — Host the website (GitHub Pages + Cloudflare — both free)

We'll use **GitHub Pages** to host the files, and **Cloudflare** to connect
your `crebrl.ai` domain to it. Both are free.

### Step 3.1 — Create a GitHub account
1. Go to **github.com** → **Sign up**. Use any email you like.

### Step 3.2 — Create a repository
1. Click the **+** icon (top right) → **New repository**.
2. Name it `crebrl-website` (any name works).
3. Set it to **Public**. Click **Create repository**.

### Step 3.3 — Upload your files
1. On the new repository page, click **uploading an existing file**.
2. Drag in **all the files and folders** from your `crebrl-website` folder
   (index.html, products.html, contact.html, styles.css, script.js, and the
   `images` folder).
3. Scroll down, click **Commit changes**.

### Step 3.4 — Turn on GitHub Pages
1. In your repository, click **Settings** (top menu).
2. In the left sidebar, click **Pages**.
3. Under "Branch," select **main** and folder **/ (root)**. Click **Save**.
4. After a minute, GitHub shows a link like:
   `https://yourusername.github.io/crebrl-website/`
5. Visit that link — your site is now live on the internet (just not yet at
   crebrl.ai).

### Step 3.5 — Connect your crebrl.ai domain

You said you've already purchased `crebrl.ai`. Now point it at your GitHub
Pages site:

1. **Add a CNAME file**: In your GitHub repository, create a new file named
   exactly `CNAME` (no extension) containing one line:
   ```
   crebrl.ai
   ```
   (Click **Add file** → **Create new file**, type `CNAME` as the name, put
   `crebrl.ai` in the content, and commit.)

2. **Update your domain's DNS settings**: Log in to wherever you bought
   `crebrl.ai` (e.g., GoDaddy, Namecheap, Google Domains). Find **DNS
   settings** / **Manage DNS**.

3. Add these records:

   | Type  | Name/Host | Value                          |
   |-------|-----------|--------------------------------|
   | A     | @         | 185.199.108.153                |
   | A     | @         | 185.199.109.153                |
   | A     | @         | 185.199.110.153                |
   | A     | @         | 185.199.111.153                |
   | CNAME | www       | yourusername.github.io         |

   (These four IP addresses are GitHub Pages' standard servers — copy them
   exactly.)

4. Back in GitHub: **Settings → Pages**, under "Custom domain," type
   `crebrl.ai` and click **Save**. Wait 10–60 minutes for DNS to propagate,
   then check the box for **Enforce HTTPS** once it becomes available.

5. Visit **https://crebrl.ai** — your site should now load with your domain
   and a secure padlock.

> **Note:** DNS changes can take anywhere from 10 minutes to 24 hours to
> take effect worldwide. If it doesn't work immediately, wait and try again.

---

## Part 4 — Set up professional email (yourname@crebrl.ai)

You have two good options. **Option A** is free but more manual. **Option
B** is paid but gives you the full Gmail/Google Workspace experience.

### Option A — Free: Cloudflare Email Routing (forwarding only)

This forwards emails sent to `hello@crebrl.ai` to your existing Gmail/personal
inbox. You **can't send from** that address without extra setup, but you can
receive everything immediately at no cost.

1. Go to **cloudflare.com** → sign up free.
2. Add `crebrl.ai` as a site (Cloudflare will scan and import your existing
   DNS records — keep the GitHub Pages records from Part 3).
3. Cloudflare gives you new **nameservers** (two addresses). Go back to your
   domain registrar and replace the existing nameservers with Cloudflare's.
4. In Cloudflare, go to **Email → Email Routing**.
5. Click **Get started**, then **Create address**: e.g.
   `hello@crebrl.ai → youremail@gmail.com`. Repeat for any team addresses
   (e.g. `bharat@crebrl.ai`).
6. Cloudflare automatically adds the required MX records.
7. To **send mail as** `hello@crebrl.ai` from Gmail (not just receive), in
   Gmail go to **Settings → Accounts → Send mail as → Add another email
   address**, and follow Gmail's verification steps (requires SMTP details
   from a provider — this is the limitation of the free option).

### Option B — Recommended: Google Workspace (~₹450–550/user/month)

Gives you a real inbox at `yourname@crebrl.ai`, Google Calendar, Drive, Docs,
etc. — fully send and receive.

1. Go to **workspace.google.com** → **Get started**.
2. Enter your business name (Crebrl AI Technologies Pvt. Ltd.), number of
   employees, and country (India).
3. When asked for a domain, choose **"I have a domain"** and enter
   `crebrl.ai`.
4. Create your first user (e.g. `bharat@crebrl.ai`) and set a password.
5. Google will ask you to **verify domain ownership**: it gives you a TXT
   record to add to your DNS. Go to Cloudflare (or your registrar) → DNS →
   add the TXT record exactly as shown.
6. Once verified, Google gives you **MX records** to add — these route
   email to Google's servers. Add them in the same DNS panel, removing any
   conflicting MX records (like Cloudflare Email Routing's, if you set that
   up).
7. Wait for DNS to propagate (up to a few hours), then log into
   **mail.google.com** with your new `yourname@crebrl.ai` address.
8. Add more team members under **Admin Console → Users → Add new user** —
   each additional user is billed monthly.

---

## Quick checklist

- [ ] Formspree account created, form ID added to `contact.html`
- [ ] GitHub account created, files uploaded to a repository
- [ ] GitHub Pages enabled, `CNAME` file added with `crebrl.ai`
- [ ] DNS A records (GitHub IPs) added at domain registrar
- [ ] crebrl.ai loads the site over HTTPS
- [ ] Email set up (Cloudflare free forwarding, or Google Workspace)
- [ ] Test: send a message through the contact form and confirm it arrives
- [ ] Test: send/receive an email at `hello@crebrl.ai` (or chosen address)

---

## Future edits

To update content later: edit the `.html` files directly (each section is
clearly commented), or come back and ask for help — describe what you'd
like changed and updated files can be generated for you to re-upload to
GitHub.
