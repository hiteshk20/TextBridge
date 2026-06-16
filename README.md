# TextBridge

A **zero-backend, encrypted, cross-device text bridge** that runs entirely on **GitHub Pages**. No APIs, no servers, no databases, no cost — ever.

## Features

- **Secure Link Mode** — paste text, encrypt it with AES-256-GCM, get a shareable link + QR code.
- **Live P2P Mode** — real-time WebRTC data channel between two devices, encrypted with a shared password.
- **No external dependencies** — everything is inline HTML/CSS/JS.
- **PWA-ready** — installable on mobile/desktop with offline support.
- **Free forever** — host on GitHub Pages with zero running cost.

## How it works

- Encryption uses the browser's **Web Crypto API** (`PBKDF2` + `AES-256-GCM`).
- In **Secure Link** mode, the encrypted payload lives in the URL hash (`#m=...&k=...`). The hash never leaves the browser, so nothing is ever sent to a server.
- In **Live P2P** mode, **WebRTC** creates a direct peer-to-peer channel. Free Google STUN servers are used for NAT traversal. Signaling (offer/answer) is done manually by copying the short codes.

## Deploy to GitHub Pages (1 minute)

1. Create a new repo on GitHub, e.g. `textbridge`.
2. Upload these files to the root:
   - `index.html`
   - `sw.js`
   - `manifest.json`
3. Go to **Settings → Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**, then choose **main** and **/(root)**.
5. Click **Save**.
6. In a few seconds your site is live at `https://yourusername.github.io/textbridge`.

## Use it

### Secure Link (recommended, works every time)
1. Open the site on your phone.
2. Paste the text and tap **Encrypt & Create Link**.
3. Copy the link or scan the QR code on your PC.
4. The PC opens the link and decrypts the text automatically.

### Live P2P (instant, no link needed)
1. Open the site on both devices.
2. Both enter the **same shared password**.
3. Device A clicks **Create Offer**, copies the code to Device B.
4. Device B pastes the offer, clicks **Create Answer**, copies the answer back to Device A.
5. Device A clicks **Connect** — now text sent from one device appears instantly on the other.

## Security notes

- The app never sends your plain text or passphrase to any server.
- In Secure Link mode, the encrypted payload is embedded in the URL. If you choose to embed the passphrase too, anyone with the link can read it — share it carefully.
- WebRTC data channels are already encrypted by DTLS; the additional AES layer ensures end-to-end privacy even if you do not trust the STUN server.

## License

MIT — free to use, modify, and deploy.
