# Soora New Year Photobox

Static web app (no build step). Customers take photos with their camera, choose a strip frame, add a name and a wish, then download a 1200x1800 PNG (4x6 inch).
Photos are NEVER uploaded. Only the name and wish (optional, with a consent checkbox) are saved to Firestore.

## Structure
- `index.html`: the whole app (HTML, CSS, JS).
- `assets/frame-cream.png` (Happy New Year) and `assets/frame-orange.png` (flight ticket): full 1080x1920 designs, each with 2 strips x 3 transparent photo holes. The 892x1342 panel inside is the 4x6 print area.
- `logos/`: logos for the page header.
- `firebase-config.js`, `firestore.rules`, `firebase.json`, `netlify.toml`: configuration.

## Camera
"Start camera session" opens the camera in the browser, counts down 3 seconds, then takes 3 photos automatically into the 3 frames.
"Retake this frame" replaces a single frame. Upload stays available as a fallback.
The camera only works over HTTPS (Netlify is HTTPS) or localhost. Inside in-app browsers (Instagram, WhatsApp) the camera is often blocked, ask customers to open the link in Chrome or Safari.

## How the frames work
Customer photos are drawn behind the frame, so the hole shape follows the design. The same 3 photos fill both strips.
Exports: **Print 4x6** crops the panel to 1200x1800 (the name goes on the ticket stub for the flight frame). **Story** exports the full 1080x1920 design with the wish and name under the panel.

## Replace or add a frame
1. Put the new 1080x1920 PNG in `assets/` (transparent holes, same panel position, or update `PANEL`).
2. In `index.html`, in `FRAMES` at the top of the script: add an entry (`src`, `shape` rrect/rect, `r` corner radius, `cols` = x of left/right hole, `ys` = y of the 3 rows, `w`/`h` hole size).
3. Add the new frame name to the `layout in [...]` list in `firestore.rules`.

## Setup
1. Firebase: create a project, enable Firestore only (no Auth/Storage). Fill in `firebase-config.js`.
2. Rules: paste the contents of `firestore.rules` in the Rules tab and Publish (or `firebase deploy --only firestore:rules`). The layout values are `cream` and `orange`.
3. GitHub: push all files. Netlify: import the repo, empty build command, publish directory `.`
4. View or export wishes in the Firebase Console (the web app cannot read them).
