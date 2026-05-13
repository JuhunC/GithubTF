# GithubTF — Firmware CI/CD Architecture

Architecture plan and documentation site for migrating from Atlassian Bamboo + Bitbucket to GitHub Enterprise Server + Actions Runner Controller on Kubernetes, designed for firmware CI/CD at corporate scale.

## What's in this repo

```
GithubTF/
├── architecture-plan.md          # Full architecture plan (markdown source)
├── architecture-diagram.html     # Standalone single-diagram viewer
├── site/                         # Documentation website (deployed to GitHub Pages)
│   ├── index.html                # Main page with all sections & diagrams
│   └── styles.css                # Site styles (light/dark aware)
└── .github/workflows/
    └── pages.yml                 # Auto-deploys site/ to GitHub Pages on push to main
```

## Deploy to GitHub Pages

1. **Create the repo on github.com** named `GithubTF` (public or private, your call — Pages works on both for paid plans; public is free).
2. **Push this directory:**
   ```bash
   cd "/Users/johnc/Documents/Claude/Projects/GithubTF"
   git init
   git add .
   git commit -m "Initial commit: architecture plan + docs site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/GithubTF.git
   git push -u origin main
   ```
3. **Enable GitHub Pages:**
   - Open the repo on github.com → **Settings** → **Pages**.
   - Under **Build and deployment**, set **Source** to **GitHub Actions**.
4. **Trigger the workflow:** the push to `main` already triggers it. You can also run it manually from the **Actions** tab → **Deploy site to GitHub Pages** → **Run workflow**.
5. **Open the site:** once the workflow finishes, the Pages URL appears in the workflow summary and at Settings → Pages. It looks like:
   ```
   https://<your-username>.github.io/GithubTF/
   ```

## View the site locally

No build step needed — it's plain HTML/CSS with Mermaid loaded from CDN.

```bash
cd site
python3 -m http.server 8000
# open http://localhost:8000
```

## Edit the content

The website content lives entirely in `site/index.html`. The full architecture plan is in `architecture-plan.md`. Diagrams are inline Mermaid blocks — to add or change one, edit the `<pre class="mermaid">...</pre>` blocks in `index.html`.

## Diagrams included

1. **High-level architecture** — flowchart showing GHES, ARC, runner pools, data layer, test systems.
2. **Runner pool isolation** — how CI / CD / HW pools are physically separated on K8s.
3. **CD gate sequence** — sequenceDiagram of release publish → tests → QGS → environment → deploy or block.
4. **Data persistence flow** — where artifacts, logs, metadata, and metrics land, with retention.
5. **HW reservation state machine** — bench acquisition, queueing, fault handling.

## License

Internal architecture documentation. Not for redistribution.
