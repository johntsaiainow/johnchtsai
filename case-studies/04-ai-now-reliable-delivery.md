# Engineering Case Study 04 — AI-NOW: Engineering for Reliable Delivery

> **GitHub Actions · CI/CD · Astro · Node.js 22 · Ubuntu · DigitalOcean · SSH/rsync · release integrity · rollback**
>
> **Source:** [AI-Now-Inc/ai-now-web](https://github.com/AI-Now-Inc/ai-now-web) · [CI workflow](https://github.com/AI-Now-Inc/ai-now-web/blob/main/.github/workflows/ci.yml) · [CD workflow](https://github.com/AI-Now-Inc/ai-now-web/blob/main/.github/workflows/deploy.yml) · [Deployment runbook](https://github.com/AI-Now-Inc/ai-now-web/blob/main/docs/operations/deployment-runbook.md)

[← Return to the engineering portfolio](../README.md)

## The engineering question

**What does it take to turn a successful build into a production release that is traceable, controlled, and recoverable?**

Writing software is only part of delivering a system. The difficult moments often come afterward: a commit passes locally but fails in CI; an older job finishes after a newer one; a deployment transfers files successfully but the site fails its health check. A production pipeline must make these states visible and refuse unsafe transitions.

AI-NOW's website is a deliberately practical case study in that discipline. The application is an **Astro static website**, but the engineering challenge is broader than front-end development: establishing a trustworthy chain from source revision to the version served over HTTPS.

This case study complements my three flagship engineering projects. **DaVinci** deals with physical control, **Local AI Chatbot** with connected intelligence, and **RetroFPGA** with the foundations of computing. **AI-NOW** addresses the delivery discipline that helps software reach users reliably. It is supporting engineering evidence—not a fourth pillar.

## System boundary

The reviewed repository snapshot includes:

- `.github/workflows/ci.yml` — continuous integration for pushes and pull requests to `main`, plus manual dispatch.
- `.github/workflows/deploy.yml` — deployment triggered by a completed CI workflow, subject to explicit safety conditions.
- `docs/operations/deployment-runbook.md` — production topology, deployment/recovery procedures, and a dated verification record.
- `package.json` and Astro application files — the site being built and delivered.

The runbook describes a **DigitalOcean / Ubuntu 24.04** production environment using **Nginx** and **Caddy**. The server-side activation script (`/usr/local/sbin/ai-now-deploy`, documented as V2.3) is **not included in the reviewed ZIP**, so its internal behavior is described from the runbook rather than independently code-reviewed here.

## Delivery architecture

```text
Developer pushes to main / opens pull request
                   |
                   v
        GitHub Actions CI
    Ubuntu 24.04 / Node.js 22
        npm ci -> Astro build
       Generated-page validation
       Placeholder-domain checks
                   |
                   v
      CI completed successfully?
                   |
        main push + repository
           identity checks
                   |
                   v
        GitHub Actions CD
     Checkout CI-tested commit
       Rebuild and revalidate
       Generate release.json
       Reject stale main SHA
                   |
                   v
      SSH + rsync to staging
        web/releases/<id>
                   |
                   v
      Server activation (V2.3)
       Verified release snapshot
        Switch current symlink
      HTTPS release verification
                   |
          failure -> rollback
```

The diagram summarizes the workflow YAML and documented server behavior. It does not claim that every server-side operation is visible in this repository.

## Design decisions and why they matter

### 1. A successful build is a gate, not a deployment command

The CI workflow installs dependencies with `npm ci`, builds the Astro site using Node.js 22, verifies expected generated HTML pages exist and are nonempty, and checks for unwanted placeholder references. The workflow runs on `ubuntu-24.04` and triggers for pushes and pull requests targeting `main`.

These are **build and output-integrity checks**. They are not a substitute for a full unit, integration, security, or browser test suite; the reviewed CI file does not show those additional suites.

### 2. Deploy only from an eligible successful CI run

The CD workflow listens for completion of the named CI workflow, then checks for success, a `push` event, the `main` branch, and the expected repository identity (`AI-Now-Inc/ai-now-web`). A successful pull-request build does **not** by itself authorize a production deployment.

### 3. Preserve commit identity

CD checks out the SHA associated with the successful CI run, generates `dist/release.json` containing a release identifier and commit SHA, and compares that SHA with the current `main` head before upload. If the branch has advanced, the workflow refuses the stale deployment.

This makes the relationship between **tested source**, **release artifact**, and **deployed version** inspectable. The runbook additionally requires the active symlink and the HTTPS-served manifest to agree.

### 4. Separate upload privileges from production activation

The workflow uses GitHub secrets for the SSH key, known-hosts, user, and host; SSH enables strict host-key checking. `rsync` uploads generated site files into a release-specific directory. A separate privileged server command performs activation using `sudo -n`.

The runbook specifies a separation between deploy-writable `web/releases/` and root-owned `web/verified/`, and states that verified releases must not be overwritten. This separation is a meaningful safeguard against treating file transfer permissions as permission to rewrite the active production state.

### 5. Design for failure, not only success

The documented V2.3 activation process validates and snapshots a release, publishes a verified snapshot, switches the `current` symlink, recreates Nginx, and checks the HTTPS release manifest. The runbook states that activation or health-check failure triggers an **attempted automatic rollback**.

Rollback is not the same as guaranteed recovery. The runbook explicitly requires investigation of failed deployments and preserves a manual recovery procedure for emergencies.

## Evidence: what is verified and what remains bounded

| Evidence | What it supports | Boundary |
| --- | --- | --- |
| [`ci.yml`](https://github.com/AI-Now-Inc/ai-now-web/blob/main/.github/workflows/ci.yml) | Reproducible build and generated-site validation | No full test-coverage claim |
| [`deploy.yml`](https://github.com/AI-Now-Inc/ai-now-web/blob/main/.github/workflows/deploy.yml) | CI-gated deployment, source SHA checks, manifest creation, SSH upload, activation command | Does not reveal the server-side script implementation |
| [Deployment runbook](https://github.com/AI-Now-Inc/ai-now-web/blob/main/docs/operations/deployment-runbook.md) | Operational topology, rollback procedures, security boundaries, verification instructions | A documented historical baseline, not a live production audit |

The runbook records a **November 2, 2026** verified baseline, with commit `4703838fa7adf3046d5c372ca57e08b8ca8cec55` and release `gh-4703838fa7ad-41493485863`. It reports isolated end-to-end deployment tests, atomic snapshot publishing, fault-injected rollback, production deployment through GitHub Actions, HTTPS manifest verification, service checks, ownership checks, and staging cleanup.

Those results are **recorded in project documentation**. I have not re-executed the workflow, inspected the current production server, or independently audited the deployment script in preparing this case study.

## Trade-offs and next engineering steps

- **Rebuild in CD:** the deployment workflow rebuilds the site from the CI-tested commit rather than downloading a single immutable CI artifact. This preserves source identity but is not equivalent to deploying the exact same build artifact. Artifact promotion with digest verification would tighten provenance.
- **Test depth:** add automated tests appropriate to the site, dependency/security scanning, and browser-level smoke tests if needed; the current YAML demonstrates output checks, not comprehensive test coverage.
- **Deployment visibility:** publish non-sensitive deployment status and failure diagnostics; keep credentials, internal host details, and recovery privileges private.
- **Operational drift:** periodically verify that the documented server script, permission model, and rollback behavior still match production.

These are improvement opportunities, not claims that they have already been implemented.

## What this demonstrates

The engineering value of this project is not that a website can be built with Astro. It is that deployment has been treated as a **system with states, gates, identities, privilege boundaries, failure modes, and recovery procedures**.

That mindset transfers beyond web delivery—to firmware release processes, hardware test automation, embedded Linux systems, and any environment where the difference between *it built* and *it is safe to ship* matters.

> **Engineering for reliable delivery means knowing not only how a release goes live, but how to prove which release is live—and what to do when the transition fails.**

---

[← Back to the three-pillar portfolio](../README.md) · [View AI-NOW source](https://github.com/AI-Now-Inc/ai-now-web)
