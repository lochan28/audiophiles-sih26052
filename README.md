# The Audiophiles — SIH 2026 project hub

Static project page for Smart India Hackathon 2026, problem statement **SIH26052**:
a real-time AI noise-cancellation system for defence radios.

Plain HTML, CSS and JavaScript. No build step, no dependencies, no bundler.

## Layout

```
public/
  index.html          the whole page (styles and script are inline, as in the original)
  demo.mp4            the demo recording  <-- drop the real file here
  images/
    spectrograms.jpg  noisy / enhanced / clean comparison
    signal-chain.jpg  radio -> Raspberry Pi 5 -> headset
```

Everything lives under `public/` because that is the folder Vercel serves as the
site root when no framework is detected — so the deploy needs no configuration.

## Viewing it locally

Open `public/index.html` in a browser. That is all.

If autoplay or the fonts behave oddly from a `file://` URL, serve the folder
over HTTP instead:

```bash
python -m http.server 8080 --directory public
```

## Dropping in the demo video

Put the MP4 at `public/demo.mp4`. Nothing else needs editing — the page already
points at it. Until that file exists the player shows its poster image instead.

The video autoplays muted and loops, which is the only way browsers allow
autoplay. The "Tap for sound" button over the bottom-left corner unmutes it;
clicking the video itself does the same.

H.264 video with AAC audio in an MP4 container plays everywhere. Keep it under
roughly 25 MB — GitHub warns above 50 MB, and a large file makes the page slow
on a phone.

## Replacing the images

Overwrite the files in `public/images/` keeping the same names, or change the
`src` in `index.html` if you use different ones. They are JPEGs (that is what the
originals were); PNG works just as well if you swap the extension in both places.

## Deploying

Push to GitHub, then on vercel.com: **Add New → Project → import this repo →
Deploy**. No settings to change. Every later push to `main` redeploys.
