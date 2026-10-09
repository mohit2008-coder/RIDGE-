# Ridge Chat — Front-End Replica

A responsive, single-file HTML recreation of the Ridge chat interface. It is intended as a self-contained front-end demo that can be opened in a modern browser without installing a framework or running a server.

> **Scope note:** This repository/file is a front-end replica, not the original Ridge application's source code. Authentication, messages, and groups are simulated in the browser. It does not connect to the original application's backend, persist data to a database, or provide real-time communication.

## Contents

- `ridge_chat_replica.html` — the complete application (HTML, CSS, and JavaScript)
- `README.md` — these setup, architecture, and testing instructions

## Major features

- Responsive desktop and mobile layout
- Sign-in and create-account form states (demo only)
- Searchable conversation list
- Chat view with local message composition
- Group creation and member selection
- Client-side filtering and UI feedback messages
- No third-party runtime dependencies

## Architecture

The application is deliberately small and runs entirely on the client:

- **HTML** defines the page structure: sidebar, authentication panel, conversation list, chat view, message composer, and group dialog.
- **CSS** provides layout, colors, responsive breakpoints, and component styling.
- **Vanilla JavaScript** handles tab switching, demo sign-in, searching, opening conversations, adding messages, creating groups, and rendering the UI.
- **In-memory state** stores the demo users, groups, active conversation, and messages. State is lost when the page is reloaded.

### Real-time communication

No real-time communication technology is currently implemented. The demo does not use WebSockets, Socket.IO, Server-Sent Events, WebRTC, or a hosted messaging service. Sending a message adds it to the current conversation in local browser memory only.

To turn this into a multi-user chat application, add a backend API and a persistent database, implement authentication and authorization, and choose a real-time transport such as **WebSockets** (or Socket.IO). For example, a production architecture could use:

1. A browser front end for the UI.
2. A backend service for authentication, conversations, group membership, and message validation.
3. A WebSocket gateway for delivering messages to connected clients.
4. A database for users, groups, and message history.

Those components are recommendations for future work; they are not included in this HTML replica.

## Requirements

For the current demo:

- A modern browser (Chrome, Edge, Firefox, or Safari)
- No Node.js, package manager, database, API credentials, or external service is required

## Installation and local setup

### Option A: Open directly

1. Download or copy `ridge_chat_replica.html` into a folder.
2. Open the file in your browser.
3. Use the sign-in or create-account form to enter the demo state.
4. Search for one of the sample people, open a conversation, and send a message.
5. Use **New group** to create a local demo group and select members.

No dependency installation is necessary because the page uses browser-native HTML, CSS, and JavaScript.

### Option B: Serve the file locally

Serving it over HTTP is optional, but can make testing closer to a normal web deployment.

With Python 3 installed, open a terminal in the directory containing the file and run:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/ridge_chat_replica.html
```

Stop the server with `Ctrl+C`.

## Dependency installation

There are no third-party dependencies and no `package.json` file.

- Runtime dependencies: none
- Build step: none
- Install command: not applicable

If you later split the page into modules or introduce a framework/backend, document the required runtime and package installation commands here.

## Configuration and environment variables

The current application has no environment variables and no external service configuration.

| Setting | Required? | Purpose |
|---|---:|---|
| Environment variables | No | No environment variables are read by this static demo |
| API URL / backend URL | No | No API requests are made |
| Database credentials | No | No database is connected |
| Authentication secrets | No | Authentication is simulated locally |
| WebSocket URL | No | No real-time transport is configured |

**Security note:** Do not use the demo sign-in form to handle real credentials. The entered username and password are not validated by a server and do not establish a secure authenticated session.

## Reproducing the application in a clean environment

1. Install a modern web browser.
2. Obtain `ridge_chat_replica.html` and place it in an empty directory.
3. (Optional) Install Python 3 if you want to serve the file locally.
4. Open the HTML file directly, or run `python -m http.server 8000` and visit `http://localhost:8000/ridge_chat_replica.html`.
5. Verify the core interactions using the checklist below.

No network connection is required after the HTML file is available, because the current page does not load external libraries or call remote APIs.

## Manual testing checklist

Run these checks in a fresh browser tab:

- [ ] The page loads without a build step or dependency installation.
- [ ] The desktop layout displays the sidebar and main conversation area.
- [ ] Resizing the browser to a narrow/mobile width produces a usable stacked layout.
- [ ] Switching between **Sign in** and **Create account** updates the form labels.
- [ ] Submitting non-empty username and password fields enters the demo signed-in state.
- [ ] **Sign out** returns the authentication panel to its initial state.
- [ ] Searching filters the sample conversation list.
- [ ] Selecting a person opens that conversation.
- [ ] Sending a non-empty message displays it in the conversation.
- [ ] **New group** opens the group dialog.
- [ ] Member selection can be toggled.
- [ ] Creating a group adds it to the conversation list and opens it.
- [ ] Reloading the page resets demo messages and groups, as expected for in-memory state.
- [ ] The browser console has no unexpected JavaScript errors during these flows.

### Automated testing

No automated test runner is configured for this static demo. The checklist above is the baseline acceptance test. If automated regression testing is needed, add a browser test framework such as Playwright and cover the same interactions.

## Troubleshooting

- **The file opens as plain text:** ensure the filename ends in `.html`, not `.txt`.
- **The page appears blank or interactions fail:** open the browser developer tools and inspect the Console for JavaScript errors.
- **The group or messages disappear after refresh:** this is expected; data is stored in memory and is not persisted.
- **Sign-in does not validate real accounts:** authentication is only a visual demo; no identity provider or backend is connected.

## Limitations and next steps

This replica reproduces the front-end interaction flow, not the original application's full behavior. Before using it as a real chat product, implement and test:

- Secure server-side authentication and session management
- Authorization checks for direct and group conversations
- Persistent user, group, and message storage
- Real-time delivery (for example, WebSockets or Socket.IO)
- Input validation, abuse controls, rate limiting, and error handling
- Automated tests and production deployment configuration
