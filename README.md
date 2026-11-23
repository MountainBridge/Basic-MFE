# Basic-MFE · Micro-frontends with Module Federation

A minimal, readable example of splitting one Angular app into a **shell (host)** and a **remote (mfe1)** using Webpack 5 Module Federation. The shell loads the remote's `TodoModule` at runtime, only when the user navigates to `/todo`.

## Why this exists

Large front ends slow teams down when every change ships through one build. Module Federation lets separate teams build and deploy parts of the UI independently, while users still see one app. This repo strips the idea down to the smallest working version so the moving parts are easy to see.

## How it fits together

```text
 browser ──► shell (host, :4202)
               │  route ''      → HomeComponent
               │  route 'todo'  → import('mfe1/TodoModule')   (lazy, at runtime)
               ▼
            mfe1 (remote, :4203)
               exposes './TodoModule' via remoteEntry.js
               shares @angular/* as singletons
```

| Piece | File | What to look at |
|---|---|---|
| Remote config | `projects/mfe1/webpack.config.js` | `exposes` and the `shared` singletons |
| Host routing | `projects/shell/src/app/app-routing.module.ts` | `loadChildren` importing `mfe1/TodoModule` |
| Async bootstrap | `projects/*/src/main.ts` → `bootstrap.ts` | Why the app bootstraps in a separate file |

## Run it

```bash
npm install
npx ng serve mfe1    # remote on http://localhost:4203
npx ng serve shell   # host   on http://localhost:4202
```

Open http://localhost:4202 and click through to **Todo**. In DevTools → Network you'll see `remoteEntry.js` load from :4203 only at that moment.

## Trade-offs worth knowing

- **Shared dependencies:** Angular must be a singleton across host and remote, or you get two copies and confusing runtime errors.
- **Version drift:** independent deploys are the point, but contract changes to an exposed module need versioning.
- **When not to use it:** for a single small team, a well-structured monorepo is usually simpler.

## Stack

Angular 11 · Webpack 5 Module Federation · `@angular-architects/module-federation`

---

Part of [Nidhi Verma's engineering notes](https://github.com/MountainBridge). More patterns in the [Engineering Casebook](https://github.com/MountainBridge/MountainBridges).
