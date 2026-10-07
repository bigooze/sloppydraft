# sloppydraft

sloppydraft is a browser-based strict rough-draft typewriter. It autosaves your work in the browser and exports it as a plain-text `.txt` file.

Backspace and Delete never erase text. Instead, they wrap the affected word in square brackets, so marked text exports as `[word]`. Repeated deletion attempts do not add extra brackets.

Use the font toggle to switch between the default serif typeface and Courier. Dark mode uses green text in the writing area; light mode is also available.

Use the arrow button in the toolbar to hide the branding and controls for a distraction-free writing view. The menu button reappears in the top-right corner; the visibility choice is saved in your browser.

Export regularly. Clearing your browser storage may erase locally saved work.

Use Export to copy the writing, download it as a `.txt` file, or send a copy to Dropbox. Dropbox uploads go directly from your browser to your Dropbox account; this app does not host the uploaded file. The first Dropbox save asks you to authorize access, then places the file in the app's Dropbox folder.

To enable Dropbox uploads, configure the Dropbox app with the `files.content.write` permission and app-folder access. Register the deployed page URL as an OAuth redirect URI. The Dropbox app key is used in the browser with PKCE; access tokens are kept only for the current browser tab session.

To erase the current document and its saved work name, press the flame button five times within five seconds. This does not change your appearance preferences.
