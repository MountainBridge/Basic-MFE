# Basic MFE — Module Federation Proof of Concept

> A historical Angular microfrontend experiment reframed as an architecture and independent-delivery case study.

## 30-second read

This repository explores **microfrontend boundaries, runtime composition and independent application delivery**. The 2026 treatment preserves the original proof of concept while making the engineering questions explicit.

**Primary question:** when does splitting a frontend into independently delivered applications create real value, and when does it only create operational complexity?

## Architecture

```text
                    Host / Shell
                         |
              Module Federation boundary
                    /           \
                   /             \
            Remote A           Remote B
             Angular             Angular
                 \               /
                  \             /
                   shared contracts
```

## What this demonstrates

- Angular application boundaries
- Webpack 5 Module Federation
- remote/host composition
- shared dependency concerns
- independent deployment trade-offs
- frontend integration failure modes

## Run it online

**[Open in GitHub Codespaces](https://codespaces.new/MountainBridge/Basic-MFE)** — recommended full-project environment.

**[Open in StackBlitz](https://stackblitz.com/github/MountainBridge/Basic-MFE)** — browser playground for inspecting/running the project. Because this is a historical Angular/Module Federation stack, Codespaces is the authoritative path if the browser sandbox hits version constraints.

## Run locally

```bash
npm install --legacy-peer-deps
npm start
```

Then follow the host/remote ports exposed by the application.

## Failure-first questions

| Scenario | What we need to prove |
|---|---|
| remote unavailable | Does the shell degrade gracefully? |
| incompatible shared dependency | Can independently released teams coexist? |
| remote version mismatch | How are contracts/versioning handled? |
| slow remote | What is the UX fallback? |
| deployment rollback | Can one remote be rolled back independently? |
| duplicated dependencies | Is the runtime actually gaining efficiency? |

## Modernization path

```text
POC
 ↓
Define ownership boundaries
 ↓
Define contracts + compatibility policy
 ↓
Independent CI/CD
 ↓
Failure handling + observability
 ↓
Performance measurement
 ↓
Decide whether MFE complexity is justified
```

## Interview prompts

1. Why Module Federation instead of a monolith?
2. What should and should not be shared?
3. How do you version a remote contract?
4. What happens when a remote fails after the shell has loaded?
5. How would you measure whether MFE improved delivery rather than just architecture diagrams?
