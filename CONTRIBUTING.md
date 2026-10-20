# Contributing

Card Stack Trainer is a dependency-free progressive web app. Changes should
keep the repository directly deployable as a static site.

## Development

1. Start a local server with `python3 -m http.server 8000`.
2. Open <http://localhost:8000>.
3. Make the smallest change needed in `index.html`, `manifest.webmanifest`, or
   `sw.js`.
4. If a cached file changed, update `VERSION` in `sw.js`.

The `src/...` comments in the script identify logical module boundaries. Keep
new code with the relevant module and preserve those markers so the bundled
file remains navigable.

## Manual checks

There is currently no automated test suite. Before publishing a change, check:

- The home, Learn, Challenges, Stats, Settings, and Stacks screens open.
- Mnemonica, Aronson, Si Stebbins, and custom stacks can be selected.
- Practice accepts answers and records progress.
- English and French labels render correctly.
- Theme selection works in light and dark mode.
- A backup can be exported and restored.
- Reloading preserves settings and progress.
- The app loads offline after one successful online visit.
- The browser reports a valid web app manifest and no console errors.

When testing service-worker changes, close all app tabs or unregister the old
worker and clear site data to avoid mistaking stale cached files for current
ones.

## Scope

Keep the app usable without a server, account, build tool, or third-party
runtime dependency. Do not commit personal backups, browser data, generated
debug output, or credentials.
