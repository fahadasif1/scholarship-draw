# Lucky draw (draw.convosoft.uk)

Projector page for the live 100% Master's scholarship draw, one winner per city, drawn from checked-in guests.

- Static page (`index.html`, `config.js`, `CNAME`). No keys and no student data in the files. Staff type the access key on the night; it is not stored.
- Pool = the scanner sheet's **Scanned** tab, minus Scorp Staff, minus repeat names, minus earlier winners (backend action `pool`).
- Pick: the pool locks when Draw is pressed (fingerprint shown). Each director presses a hidden number 0-9 (1 to 8 directors, set on the set-up screen); digits are revealed together. Winner = SHA-256(digits + pool fingerprint + fresh 128-bit browser random) mod pool size. Digits and the random value are written to the Draw Log note.
- Every result is written to a **Draw Log** tab (DRAWN, WINNER, REDRAW with reason) via backend action `drawlog`. Nothing else in the sheet is changed.
- **Practice** option: dummy names, nothing saved. Rehearse before doors.
- Backend code: `manchester-scanner/backend-birmingham/Code.gs` (actions `pool`, `drawlog`; tests in `test-backend.js`).

## To go live (all need Fahad's OK)
1. Deploy the new Birmingham backend version (Deploy › Manage deployments › edit › New version, never a new deployment), then put its /exec address in `config.js`.
2. New GitHub Pages repo for this folder, custom domain draw.convosoft.uk, Cloudflare DNS-only CNAME `draw` → fahadasif1.github.io.
3. Rehearse with Practice, then with the real sheet before the doors open.
