# Northline — Dummy Project

A minimal static site used as a demo/scaffold. Four pages, one stylesheet, no build step.

```
dummy-project/
├── index.html          Home
├── about.html           About
├── project.html         Project
├── contact.html          Contact Us
├── css/
│   └── style.css
└── .github/
    └── workflows/
        └── deploy.yml    CI/CD pipeline (GitHub Actions)
```

Open `index.html` directly in a browser — no server or install needed.

## CI/CD pipeline, in brief

`.github/workflows/deploy.yml` sets up a simple **CI/CD pipeline** using GitHub Actions:

1. **Trigger** — the pipeline runs automatically on every push to `main`, and also on pull requests targeting `main` (so problems surface before merge).
2. **CI (Continuous Integration)** — the `build-and-test` job checks out the code and runs an HTML validator. In a real app this is where you'd install dependencies and run your test suite (`npm ci && npm test`, `pytest`, etc.).
3. **CD (Continuous Deployment)** — the `deploy` job only runs if `build-and-test` succeeds (`needs: build-and-test`) and only on a push to `main` (not on PRs). It uploads the site as a Pages artifact and deploys it with `actions/deploy-pages`.

The core idea of any CI/CD pipeline is the same regardless of tooling:

| Stage | Purpose |
|---|---|
| Trigger | Decide *when* the pipeline runs (push, PR, tag, schedule) |
| Build | Install dependencies, compile/bundle if needed |
| Test | Run automated checks; fail fast if something's broken |
| Deploy | Ship the validated code to staging/production, only if prior stages passed |

### To use this yourself
1. Push this project to a GitHub repo.
2. In the repo settings, go to **Pages** → set source to **GitHub Actions**.
3. Push to `main` — the workflow will run and publish the site automatically.

Swap the validator/test step for whatever your real project needs (`npm test`, `pytest`, `docker build`, etc.) — the trigger → build → test → deploy shape stays the same.
