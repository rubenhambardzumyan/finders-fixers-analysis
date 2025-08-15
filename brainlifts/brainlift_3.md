Web Extension Development

- **Owner:** Denys Yefimenko
- **Purpose:**
  - Capture current best practices of Web Extension development and establish a reusable baseline for BrainLift-aligned projects.
  - **Out of scope:** Deep browser‑engine internals that frameworks already abstract; app‑specific backend systems; generic UI/UX theory; non‑extension, general web‑app guidance.

## DOK4 — SPOVs (Spiky Points of View)

- Hand‑edited manifests are malpractice in 2025 — use WXT/Plasmo (or equivalent) or expect flaky, single‑browser builds.
- React in content scripts is an anti‑pattern. Use Web Components/vanilla for in‑page UI; reserve React/Preact for isolated UIs (popup/options/pages).
- Treat storage as your event bus. Prefer `storage.onChanged` for state fan‑out; use `runtime.sendMessage` only for commands/queries.
- If your design needs a “kept‑alive” background, your design is wrong. Embrace ephemeral service workers/event pages and idempotent handlers.
- Runtime origin permissions > broad install‑time host permissions. Ask late, narrowly, and only when needed.
- **Build for multi‑browser from day one.** “Chrome‑only” ships tech debt; test in Firefox early to flush CSP/API assumptions. Use `browser.*` APIs instead of `chrome.*` *. *Leverage frameworks for interoperability.
- Ban shared mutable singletons across entrypoints. Synchronize via events and reducers, not globals.
- **Design like a distributed system.** Add a version field to every message/schema. Make handlers idempotent with unique message IDs. Retry with backoff. Sync state via storage.onChanged, not direct pings. Design UX for eventual consistency. Skip this and your data flow will eat your product.
- **If you’re not hijacking the page’s runtime, you have no business in the page world.**
  - Page-world scripts exist for one job: patch, intercept, and inspect the site’s own JS. Everything else belongs in content scripts or workers.
  - Hard rules:
  - Only ship page-world code to hook (fetch, XHR, events), read/write window globals, or monkey-patch app functions.
  - Keep it stateless and tiny (<2KB)—no business logic, no state, no API calls.
  - Communicate out via postMessage with explicit schema + version; never reach back directly.
  - If a task doesn’t require touching page JS objects, don’t inject—do it in a content script.
- **In extensions, Redux is a cache** — not the source of truth. Make the service worker + extension storage the **canonical state**; hydrate UI stores from storage, and write via commands to the worker. Direct UI → storage writes are exceptions, not defaults.

## DOK3 - Insights

- Quotas dictate architecture. storage.sync (and some stores’ review rules) enforce size/rate limits; buffer writes, batch, and back off. Treat persistence as eventually consistent.
- Cold starts cause real bugs. Worker spin‑up + tab timing leads to lost messages; design handshake/retry logic and prefer idempotent operations.
- Don’t fight CSP. Inline scripts and ad‑hoc module loading frequently fail across sites; build standalone content/page bundles and inject page‑world bridges when needed.
- Broadcast channels help UI coordination (popup/options/pages), but they don’t replace a single source of truth; they should mirror state, not own it.
- Declarative vs intercepting APIs diverge by vendor. Prefer declarative when available (privacy/perf), but abstract behind an adapter to support Firefox/Safari gaps.
- Page‑world bridges are powerful but brittle. Stabilize with a typed contract, versioned messages, and feature detection; never rely solely on DOM structure.
- Version everything. Messages, storage records, and IndexedDB schemas need explicit versioning + migrations; assume mixed‑version clients during rollout.
- Think offline‑first—even in extensions. Tabs, windows, and workers drop in and out; use event logs + reducers to reconstruct state deterministically.
- **Redux in UIs must be eventually consistent with worker state.** Treat Redux as a read‑through/write‑through cache: hydrate on mount from storage, reconcile via storage change events, and mutate through worker commands.
- **Beware Redux‑persist‑style mirroring.** Full‑state persistence to `storage.sync` quickly hits quotas and causes thrash; persist only minimal, serializable UI state and derive the rest from canonical worker data.

## Experts

- Rob Wu — Chrome extension security & API expert; frequent contributor on MV3, CSP, and messaging. [https://github.com/Rob--W](https://workflowy.com/s/engineer-brainlifts/YIgj2vOAMrsdwNUT)
- Luca Greco (rpl) — Mozilla Add‑ons engineer; core WebExtensions contributor. [https://github.com/rpl](https://workflowy.com/s/engineer-brainlifts/YIgj2vOAMrsdwNUT)
- Nathan Bierema — Maintainer of Redux DevTools browser extension; deep experience with complex stateful UIs. [https://github.com/Methuselah96](https://workflowy.com/s/engineer-brainlifts/YIgj2vOAMrsdwNUT)
- Nikolaos Pantelaios — Author of “Manifest V3 Unveiled: Navigating the New Era of Browser Extensions.” [https://arxiv.org/abs/2404.08310](https://workflowy.com/s/engineer-brainlifts/YIgj2vOAMrsdwNUT)

## Knowledge Tree

- DOK2 Summary: Extensions consist of Service Worker, content scripts, page scripts, and UI surfaces (popup, options, pages). Each context has distinct capabilities and bundling targets.
  - Source: [https://developer.chrome.com/docs/extensions](https://developer.chrome.com/docs/extensions)
  - DOK1 Facts:
    - Service Worker (MV3) is non‑persistent; responds to events and shuts down shortly after.
    - Content scripts run in an isolated world; can read/modify the DOM but have limited direct access to page globals.
    - Page scripts run in the page world; required for interacting with page‑global objects; must be injected.
    - Popup, options, and other pages are regular web apps bundled into the extension.
- DOK2 Summary: Treat SW as ephemeral. Persist with `browser.storage.local` or `browser.storage.sync` (or `chrome.*` where required) or `IndexedDB` ; cache in‑memory only for the worker’s lifetime.
  - Source: [https://developer.chrome.com/docs/extensions/develop/concepts/service-workers](https://developer.chrome.com/docs/extensions/develop/concepts/service-workers)
  - DOK1 Facts:
    - Do not rely on SW global variables for critical state.
    - Avoid trying to keep the SW alive artificially—it violates MV3 principles.
    - Choose sync for cross‑device small data; local/IndexedDB for larger, per‑device data.
- DOK2 Summary: Use complementary channels: direct messaging for commands; storage‑watcher for state; bridge to page globals with injected scripts.
  - Source: [https://victoronsoftware.com/posts/message-passing-in-chrome-extension/](https://victoronsoftware.com/posts/message-passing-in-chrome-extension/) [https://developer.chrome.com/docs/extensions/develop/concepts/messaging](https://developer.chrome.com/docs/extensions/develop/concepts/messaging)
  - DOK1 Facts:
    - `browser.runtime.sendMessage` or `onMessage` supports request/response.
    - `browser.tabs.sendMessage` targets a specific tab.
    - `browser.storage.onChanged` allows content scripts to “listen to store updates,” enabling SW → content fan‑out without tight coupling.
    - To access page‑global APIs, inject a page script and use `window.postMessage` to shuttle data across the isolated boundary.
    - Pattern: Storage‑watcher fan‑out
      - Source: [https://developer.chrome.com/docs/extensions/reference/api/storage](https://developer.chrome.com/docs/extensions/reference/api/storage)
      - Worker publishes canonical state → `storage.set` .
      - Consumers subscribe via `storage.onChanged` and re‑render deterministically.
    - Pattern: Page‑world bridge
      - Content script injects a page script.
      - Page and content exchange via `postMessage` on a namespaced channel.
- DOK2 Summary: Frameworks (e.g., WXT, Plasmo) provide file‑based entrypoints, manifest generation, MV2/MV3 targets, and multi‑browser builds; they eliminate chunking pitfalls for content/page scripts and set sane defaults.
  - Source: WXT — [https://wxt.dev/](https://workflowy.com/s/engineer-brainlifts/YIgj2vOAMrsdwNUT) , Plasmo — [https://docs.plasmo.com/](https://workflowy.com/s/engineer-brainlifts/YIgj2vOAMrsdwNUT) , Vite — [https://vitejs.dev/guide/](https://workflowy.com/s/engineer-brainlifts/YIgj2vOAMrsdwNUT)
  - DOK1 Facts:
    - Modern frameworks support MV2 and MV3 to maximize compatibility.
    - File‑based routing for entrypoints (content, background/worker, pages) keeps manifest in sync.
    - Built‑in CLI to build/zip/submit reduces bespoke tooling.
    - Content/page scripts are built as self‑contained bundles; workers can be chunked normally.
- DOK2 Summary: Share pure utilities carefully; avoid cross‑entrypoint imports that force chunk splits in content/page scripts. Frameworks enforce isolation.
  - DOK1 Facts:
    - Vite’s default aggressive chunking can break content/page scripts.
    - Use framework‑provided aliases/virtual modules for shared constants and types.
    - Consider duplicating tiny utilities for safety in page/content contexts.
- DOK2 Summary: Least‑privilege, runtime‑granted permissions shorten reviews across CWS (Chrome), AMO (Firefox), Edge Add‑ons, and Safari. Align requests with actual code paths.
  - DOK1 Facts:
    - Declare only necessary permissions; prefer `optional_host_permissions` and runtime grants over broad install‑time hosts.
    - Static `content_scripts` **do not require scripting;** include scripting only if you call _scripting_ APIs.
    - **Reviews fail for both missing required permissions and unused requested ones.**
    - If collecting user data, a **public privacy policy is mandatory** and must be linked in each store listing.
    - API/permission availability varies (e.g., declarativeNetRequest not universal); guard vendor‑specific permissions behind conditional builds.
- DOK2 Summary: Target pages often block inline scripts via CSP; treat content scripts as standalone, and use injected page scripts for page‑world needs.
  - DOK1 Facts:
    - Avoid eval/remote code - MV3 forbids remotely hosted executable code in the extension package.
    - Inline scripts are commonly blocked; ship code as files referenced by the manifest or injected URLs.
- DOK2 Summary: SW updates ship only with a new extension package; plan versioned releases and staged rollouts across stores.
  - DOK1 Facts:
    - The only way to update a Service Worker is to publish a new version.
    - MV3 forbids remote code loading for security.
- DOK2 Summary: Small API/behavior differences exist across Chromium/Firefox; rely on framework abstractions and conditional build targets.
  - DOK1 Facts:
    - WXT can target multiple browsers from one codebase.
    - Test critical flows in each target browser before release.
- DOK2 Summary: In extension UIs (popup/options/content) backed by React + Redux, treat Redux as an ephemeral UI cache hydrated from and synchronized to a canonical state owned by the service worker and persisted in extension storage. Use declarative subscriptions to storage change events for fan‑out and command‑based messaging for mutations.
  - DOK1 Facts:
    - A Redux store lives in a single JS execution context and is not shared across extension contexts; each page/worker has its own memory.
    - `browser.storage.onChanged` notifies all extension contexts when stored items change, enabling cross‑context state updates.
    - Extension service workers are non‑persistent and must not rely on globals for durable state.
    - `storage.sync` enforces item and total size quotas, making naive full‑state mirroring impractical.
    - UI surfaces should initialize (hydrate) their Redux store from storage on mount and reconcile via change events for subsequent updates.
