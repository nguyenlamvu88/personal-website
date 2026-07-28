# Personal Website Deployment Notes

This repository contains my personal portfolio website and documents how it is published from GitHub through Render and connected to my custom domain through Bluehost.

## Live Websites

- Custom domain: `https://vuops.com`
- Render site: `https://vu-nguyen.onrender.com`
- GitHub Pages copy: `https://nguyenlamvu88.github.io/personal-website/`

## Deployment Architecture

```text
GitHub repository
nguyenlamvu88/personal-website
        |
        | push/commit to main
        v
Render static site
vu-nguyen.onrender.com
        |
        | custom-domain DNS
        v
Bluehost-managed domain
vuops.com
```

GitHub stores the source files. Render builds and hosts the primary live website. Bluehost manages the domain registration and DNS records that point `vuops.com` to Render.

GitHub Pages also publishes a separate copy of the website from the repository root.

## GitHub Repository

Repository:

```text
nguyenlamvu88/personal-website
```

Primary branch:

```text
main
```

Important files and folders:

```text
personal-website/
├── index.html
├── index_html/
│   └── index.html
├── images/
├── resume/
├── README.md
└── other project files
```

### Important

GitHub Pages requires this file at the repository root:

```text
/index.html
```

The repository also contains:

```text
/index_html/index.html
```

Keep both copies synchronized until the Render **Publish Directory** is confirmed in:

```text
Render → vu-nguyen → Settings
```

The root `index.html` is the copy used by GitHub Pages when Pages is configured for:

```text
Branch: main
Folder: / (root)
```

## Normal Website Update Process

### 1. Update the HTML

Edit the latest portfolio HTML and save it as:

```text
index.html
```

Before publishing, verify:

- Navigation links work
- Portrait loads
- Résumé link works
- Interactive map loads
- Map markers are clickable
- Experience Timeline renders correctly
- Project cards are in the correct order
- The page works on desktop and mobile

### 2. Update GitHub

Upload or edit the root file:

```text
/index.html
```

Commit to:

```text
main
```

Example commit message:

```text
Update portfolio layout and experience timeline
```

If Render still uses the `index_html` directory, update this file too:

```text
/index_html/index.html
```

### 3. Confirm GitHub Pages

GitHub Pages settings:

```text
Repository → Settings → Pages
```

Expected configuration:

```text
Source: Deploy from a branch
Branch: main
Folder: / (root)
```

After the deployment finishes, verify:

```text
https://nguyenlamvu88.github.io/personal-website/
```

Use a hard refresh when needed:

```text
Ctrl + Shift + R
```

### 4. Confirm Render Deployment

Render service:

```text
vu-nguyen
```

Connected repository:

```text
nguyenlamvu88/personal-website
```

Connected branch:

```text
main
```

Render dashboard path:

```text
Render Dashboard → vu-nguyen
```

Render should deploy automatically after a commit to `main`.

If it does not:

```text
Manual Deploy → Deploy latest commit
```

If the old version remains:

```text
Manual Deploy → Clear build cache & deploy
```

Verify the Render copy at:

```text
https://vu-nguyen.onrender.com/
```

### 5. Confirm the Custom Domain

After Render shows the updated website, verify:

```text
https://vuops.com
```

Use:

```text
Ctrl + Shift + R
```

Bluehost does not host the HTML in this setup. Bluehost manages the domain and DNS only.

## Bluehost Configuration

Domain:

```text
vuops.com
```

Nameservers are managed through Bluehost.

The Bluehost DNS records point the custom domain to Render. At the time this setup was documented, the relevant records included:

```text
A record
Host: @
Points to: Render IP address

CNAME record
Host: www
Points to: vu-nguyen.onrender.com
```

Do not change these records unless the Render custom-domain instructions change.

Bluehost sections such as the following do not edit the website HTML:

- Domains
- Nameservers
- DNS
- Contacts
- Move & Access

The website content is updated through GitHub and deployed through Render.

## How to Verify Everything Is Connected Correctly

### GitHub to Render

In Render:

```text
vu-nguyen → Settings
```

Confirm:

```text
Repository: nguyenlamvu88/personal-website
Branch: main
```

Compare the latest Render deployment commit with the latest GitHub commit.

### Render to Bluehost Domain

Confirm that:

```text
https://vu-nguyen.onrender.com/
```

and:

```text
https://vuops.com
```

show the same website.

If Render is updated but `vuops.com` is not, the issue is usually browser or DNS caching rather than the HTML.

## Current Website Publishing Roles

| Service | Purpose |
|---|---|
| GitHub | Stores the website source code |
| GitHub Pages | Publishes a separate GitHub-hosted copy |
| Render | Hosts the primary live static website |
| Bluehost | Manages the `vuops.com` domain and DNS |

## Common Problems

### GitHub Pages shows only the README title

Cause:

```text
No index.html exists at the selected publishing root.
```

Fix:

```text
Add /index.html to the repository root.
```

### Render shows an old version

Try:

```text
Manual Deploy → Deploy latest commit
```

Then:

```text
Manual Deploy → Clear build cache & deploy
```

### The custom domain shows an old version

First confirm Render is updated, then hard refresh:

```text
Ctrl + Shift + R
```

Also test in an Incognito window.

### The portrait or résumé does not load

Check that the linked files still exist at the exact paths referenced in `index.html`, especially under:

```text
/images/
/resume/
```

### GitHub Pages and Render show different versions

Likely cause:

```text
GitHub Pages is using /index.html
Render may be using /index_html/index.html
```

Check Render’s **Publish Directory** and synchronize both copies if necessary.

## Recommended Future Cleanup

Once the Render Publish Directory is confirmed, simplify the repository so there is only one authoritative homepage file.

Preferred structure:

```text
personal-website/
├── index.html
├── images/
├── resume/
└── README.md
```

Then configure both GitHub Pages and Render to publish from the repository root.

## Quick Update Checklist

```text
[ ] Update index.html
[ ] Test locally
[ ] Commit changes to main
[ ] Confirm GitHub Pages deployment
[ ] Confirm Render deployment
[ ] Confirm vu-nguyen.onrender.com
[ ] Confirm vuops.com
[ ] Hard refresh if needed
```

## Security and Privacy Notes

- Do not publish screenshots that expose personal contact information.
- Bluehost Domain Privacy should remain enabled when available.
- Avoid placing sensitive information, credentials, API keys, or private documents in this public repository.
- An active security-clearance status may change over time; update the portfolio text when necessary.
