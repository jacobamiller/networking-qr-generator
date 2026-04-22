# Networking Event vCard QR Code Generator – MVP & Roadmap

You are building a networking tool for generating shareable QR codes that encode vCards with meeting context. This starts as a mobile-first web app hosted on GitHub Pages.

## Project Concept

At a networking event, the user wants to hand out a QR code that, when scanned by another attendee, adds the user's contact info to the attendee's address book. The vCard includes a note field populated with event context (e.g., "You met Kevin at TechCrunch Disrupt on April 30, 2026") so the attendee can remember who the user is days later when reviewing contacts.

The note is for the *attendee*, not about them. The same QR code is handed out to everyone at a given event.

## MVP Beta Requirements

Build a single-page web application with the following structure:

### 1. Profile Section (Low-Friction Editing)
- Store vCard details: full name, email, phone, company, job title
- Hide behind an "Edit Profile" button or modal — changes should be deliberate, not accidental
- Pre-populate from localStorage on load
- User only needs to fill this out once

### 2. Event QR Code Generator (Main Interface)
- Form with three inputs:
  - **Date field**: auto-populate with today's date (editable)
  - **Location/Event Name**: where the user is attending
  - **Notes box**: custom text that goes into the vCard note field
- "Generate QR Code" button
- Display QR code prominently at the top of the screen (so it's easy to show someone)
- Show the note text below the QR code so the user can see what scanners will receive
- Each update to notes and button click generates a fresh QR code
- The QR code should persist on screen for the duration of the event (no auto-clearing)

### 3. vCard Encoding
- Standard vCard (.vcf) format containing: name, email, phone, company, title, and note field
- Note field includes: date, location, and custom text from the notes box
- QR code encodes the vCard so scanning adds the contact directly to the scanner's address book
- Must work on both iOS and Android native contacts apps

### 4. History Page
- Reverse-chronological list of all generated QR codes
- Display only the note text for each entry (the text that was in the vCard note field)
- No QR thumbnails, no filtering, no search — just a clean list
- Store history in localStorage

### 5. Mobile-First Design
- Optimized for mobile screens first
- Clean, minimal UI
- QR code large and easy to show someone at arm's length

### 6. Security & Privacy
- GitHub repository must be **private** — only the user has access to the code
- All data stored locally in browser localStorage, never sent to a server
- No backend or login required for MVP
- When scaling to multi-user in Phase 1, implement authentication and persistent backend storage

### 7. Tech Stack
- Use any modern framework (React with Vite is fine, or plain HTML/JS if simpler)
- Use a well-maintained vCard library (e.g., `vcard-creator` or `vcf`) for standards-compliant vCards
- Use a well-maintained QR code library (e.g., `qrcode.react` or `qrcode`) for QR code generation
- All data persists to localStorage; no backend required

### 8. GitHub Setup Instructions
Include clear step-by-step instructions in a README.md for the user to:
1. Create a new **private** repository on GitHub named `networking-qr-generator` (or user's choice)
2. Initialize the local project as a git repository
3. Add the remote origin pointing to the GitHub repo
4. Push the initial code to GitHub
5. Enable GitHub Pages in the repository settings, pointing to the main branch (or `gh-pages` branch if using a deploy action)
6. Configure base URL / homepage in the project config so assets load correctly from the GitHub Pages subdomain
7. Provide the live URL format where the app will be accessible (e.g., `https://<username>.github.io/networking-qr-generator/`)

Also include a local development section explaining how to run the app locally before deploying:
- `npm install`
- `npm run dev` (or equivalent)
- How to build for production (`npm run build`)

## Success Criteria for MVP
- User fills in profile once, stored locally
- User generates a QR code for an event in under 30 seconds
- QR code scans and adds the user's contact to an attendee's address book with the event note visible in the contact's notes field
- History page displays past events in reverse chronological order
- Entire app is deployable to GitHub Pages with clear instructions

## Future Roadmap (For Context, Not MVP)

- **Phase 1**: Multi-user platform with login and persistent database backend (Firebase, Supabase, or similar) to save vCard details and event history across devices
- **Phase 2**: Dual vCard support — personal and business profiles the user can switch between
- **Phase 3**: Calendar reminder system for attendees (either a second QR code encoding an iCalendar event, or a web-based follow-up flow sent from the server)
- **Phase 4**: Analytics dashboard showing scan counts per QR code
- **Phase 5**: Native iOS and Android mobile app wrappers around the web app
- **Phase 6**: Stale-note warning — if the currently generated note is more than 12 hours old, show a warning prompting the user to refresh it before handing out the QR code