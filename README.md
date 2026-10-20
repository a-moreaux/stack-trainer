# Card Stack Trainer

A small, installable web app for learning a memorized deck of playing cards.

Card Stack Trainer includes the Mnemonica and Aronson stacks, supports custom
stacks, and offers flashcards, practice questions, timed challenges, progress
tracking, and weak-card review. The interface is available in English and
French.

## Highlights

- Learn cards by position, card, or a mixture of both
- Practice card-to-position, position-to-card, and neighboring-card recall
- Work through timed challenges and track stars, accuracy, and response times
- Use built-in Mnemonica and Aronson stacks or create a custom 52-card stack
- Generate and recognize Si Stebbins stacks
- Export and restore local backups
- Install the app and use it offline
- Follow the device theme and language, with manual overrides

## Use the app

Open the deployed site in a modern browser. To install it, use the browser's
**Add to Home Screen** or **Install app** action.

All settings, custom stacks, and training progress are stored in the browser's
local storage. The app has no account, server, analytics, or network API. Data
does not leave the device unless the user copies a backup.

## Run locally

No build step or dependencies are required. Serve the repository root over
HTTP:

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>. Serving over HTTP is important because
service workers are not available when the page is opened directly with a
`file://` URL.

## Repository layout

```text
.
├── index.html            # Complete UI, styles, application logic, and translations
├── manifest.webmanifest  # Install metadata for the progressive web app
├── sw.js                 # Offline cache and update behavior
├── icon-180.png          # Apple touch icon
├── icon-192.png          # Browser/PWA icon
├── icon-512.png          # Large and maskable PWA icon
├── CONTRIBUTING.md       # Maintenance workflow and manual test checklist
└── README.md
```

The application is deliberately shipped as one self-contained HTML file. This
keeps static hosting simple and allows the repository root to be deployed
directly, including with GitHub Pages. Inside `index.html`, comments such as
`src/core/cards.js` and `src/ui/screens/learn.js` mark the logical module
boundaries in the bundled script.

### Runtime structure

- **Core modules** model cards and stacks, build questions, manage sessions,
  calculate progress, and serialize browser state.
- **UI modules** render reusable controls and screens with a small DOM helper.
- **Application shell** handles navigation, persistence, language selection,
  and service-worker registration.
- **Service worker** precaches the page, manifest, and icons for offline use.

## Browser data

The app saves its state in `localStorage`. If storage is unavailable, it falls
back to in-memory storage for the current session. Clearing site data removes
saved progress and custom stacks, so use the in-app backup feature before
clearing browser storage or moving to another device.

## Updating the app

After changing any cached asset, update `VERSION` in `sw.js`. A new cache name
allows the service worker to remove the old cache and serve the updated files.
If a new runtime file is added, also add it to `FILES`.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the maintenance checklist.

## Compatibility

The app targets current versions of Safari, Chrome, Edge, and Firefox. PWA
installation details vary by browser and operating system. Offline support
starts after the first successful online visit.
