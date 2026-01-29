# Copilot instructions for this repo

## Project structure & intent
- This repo is an n8n community node package. Nodes live in `nodes/` and credentials in `credentials/`.

## Declarative node pattern (recommended for HTTP APIs)
- Node entrypoints define `requestDefaults` and `properties` arrays in the node class file under `nodes/`.
- Operations are defined in resource modules under `nodes/**/resources/**` using `routing.request` blocks (method + URL templating).
- Parameter definitions are composed from shared descriptors in `nodes/**/shared/**` (e.g., `resourceLocator` modes, validations, and URLs).
- Pagination is wired via `routing.operations.pagination` and helper utilities from `nodes/**/shared/**`.
- Dynamic dropdowns use `listSearch` methods in `nodes/**/listSearch/**` and are registered under `methods.listSearch` in the node class.
- Auth is handled via `helpers.httpRequestWithAuthentication` in shared transport helpers under `nodes/**/shared/**` with credential types from `credentials/`.

## Imperative node pattern (custom logic)
- For custom logic, implement `execute()` and use `NodeOperationError` for item-level failures.

## Build & dev workflow
- Dev: `npm run dev` (runs `n8n-node dev` with hot reload).
- Lint: `npm run lint` or `npm run lint:fix`.
- Build: `npm run build` (outputs `dist/`).

## Project-specific conventions
- Register new nodes and credentials in `package.json` under `n8n.nodes` and `n8n.credentials` (point to `dist/...`).
- Keep icons in `icons/` and reference them via `icon: { light: 'file:...', dark: 'file:...' }`.
- Prefer declarative `routing` blocks and shared descriptors for HTTP APIs; only use `execute()` when necessary.
