# Soora New Year Photobox

Static web app (no build step). Customers take photos with their camera, choose a strip frame, add a name and a wish, then download a 1200x1800 PNG (4x6 inch).
Photos are NEVER uploaded. Only the name and wish (optional, with a consent checkbox) are saved to Firestore.

## Structure
- `index.html`: the whole app (HTML, CSS, JS).
- `assets/frame-cream.png`, `assets/frame-orange.png`: strips from the design team (transparent PNG 471x1417, photo holes are transparent).
- `logos/`: logos for the page header.
- `firebase-config.js`, `firestore.rules`, `firebase.json`, `netlify.toml`: configuration.

## Camera
"Start camera session" opens the camera in the browser, counts down 3 seconds, then takes 3 photos automatically into the 3 frames.
"Retake this frame" replaces a single frame. Upload stays available as a fallback.
The camera only works over HTTPS (Netlify is HTTPS) or localhost. Inside in-app browsers (Instagram, WhatsApp) the camera is often blocked, ask customers to open the link in Chrome or Safari.

## How the frames work
Customer photos are drawn behind the frame, so the hole shape (rounded square / oval) follows the design automatically.
The customer's wish and name are placed under each strip (each cut strip has its own caption).

## Replace or add a frame
1. Put the new PNG in `assets/` (ratio 471:1417, transparent photo holes, higher resolution is fine).
2. In `index.html`, in `FRAMES` at the top of the script: add a new entry (`src`, shape `rrect` or `ellipse`, and `slots` = [x, y, width, height] of each hole in 471x1417 pixels).
3. Add the new frame name to the `layout in [...]` list in `firestore.rules`.

## Setup
1. Firebase: create a project, enable Firestore only (no Auth/Storage). Fill in `firebase-config.js`.
2. Rules: paste the contents of `firestore.rules` in the Rules tab and Publish (or `firebase deploy --only firestore:rules`). The layout values are `cream` and `orange`.
3. GitHub: push all files. Netlify: import the repo, empty build command, publish directory `.`
4. View or export wishes in the Firebase Console (the web app cannot read them).
