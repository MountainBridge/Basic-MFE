# 2026 Engineering Evidence

This is a historical Module Federation proof of concept. Preserve it as evidence of microfrontend boundaries rather than pretending the original Angular version is current.

## Engineering questions

- What is independently deployable?
- Where is the contract between host and remote?
- What happens when a remote is unavailable or incompatible?
- How are shared dependencies versioned and isolated?
- How do CI and runtime observability expose boundary failures?

The next-generation portfolio implementation should answer those questions with current tooling, typed contracts, failure injection, and observable runtime behavior.

## Reproduce

```bash
npm ci --legacy-peer-deps
npm run build -- --configuration production
npm test -- --watch=false --browsers=ChromeHeadless
```
