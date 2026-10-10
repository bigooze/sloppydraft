# sloppydraft

sloppydraft is a browser-based strict rough-draft typewriter. It autosaves your work in the browser and exports it as a plain-text `.txt` file.

Backspace and Delete never erase text. Instead, they wrap the affected word in square brackets, so marked text exports as `[word]`. Repeated deletion attempts do not add extra brackets.

Use the font toggle to switch between the default serif typeface and Courier. Dark mode uses green text in the writing area; light mode is also available.

Use the arrow button in the toolbar to hide the branding and controls for a distraction-free writing view. The menu button reappears in the top-right corner; the visibility choice is saved in your browser.

Export regularly. Clearing your browser storage may erase locally saved work.

Use Open to load a `.txt` or `.md` file from your device or from the app folder in Dropbox. Opening a file replaces the current writing after confirmation. Use Export to copy the writing, download it as a plain-text `.txt` file, or send a copy to Dropbox. Dropbox transfers go directly between your browser and Dropbox; this app does not host your files. The first Dropbox open or save asks you to authorize access.

To enable Dropbox file opening and uploads, configure the Dropbox app with app-folder access and the `files.content.read`, `files.metadata.read`, and `files.content.write` permissions. Register the deployed page URL as an OAuth redirect URI. The Dropbox app key is used in the browser with PKCE; access tokens are kept only for the current browser tab session.

To erase the current document and its saved work name, press the flame button five times within five seconds. This does not change your appearance preferences.

## Learning guide

The app is intentionally kept in one file: `index.html` contains the page structure, styles, and JavaScript. In that file, the CSS is grouped by theme, toolbar, writing area, dialogs, and responsive layout. The script has section notes to help you find the related behavior.

### Follow the data

1. **Page structure:** Find the toolbar, editor, and the import/export `<dialog>` elements. The IDs on these elements are the connection points used by JavaScript.
2. **Saved state:** On startup, the script reads the draft and preferences from `localStorage`. `saveEditor()` stores the writing and refreshes the word count; `sessionStorage` is used for short-lived Dropbox sign-in state and tokens.
3. **Editing:** The editor is a `contenteditable` element. `keydown`, `beforeinput`, and `paste` handlers intercept browser defaults. `markWord()` uses the selection and DOM ranges to mark a word instead of deleting it.
4. **File input/output:** The local-file input reads plain text with `File.text()`. Export creates a `File`; a temporary object URL makes it downloadable without a server. Imports use `textContent` so file contents become text, not executable markup.
5. **Dropbox:** `startDropboxAuthorization()` creates a PKCE challenge and redirects to Dropbox. `finishDropboxAuthorization()` validates the returned state, exchanges the authorization code, and resumes the requested action. Listing and downloading use Dropbox's API; `getDropboxAccessToken()` shares the session-token check between opening and saving.

### Try these small changes

- Change the theme color tokens near the top of the stylesheet and test both light and dark modes.
- Add a preference: read it from `localStorage` during startup, update it in a button handler, and save it when it changes.
- Trace a local import from the file input's `change` event through `loadImportedDocument()` to `saveEditor()`.
- Test the Dropbox flow using the app-folder permissions above; use the browser's Network panel to follow the list, download, and upload requests.

After changing the app, check a normal edit/reload, opening a local file, cancelling the replace confirmation, downloading a draft, and both Dropbox open and save. Dropbox testing requires the configured app and redirect URI; syntax checks alone cannot validate an OAuth round trip.
