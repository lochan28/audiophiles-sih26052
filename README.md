# The Audiophiles — SIH 2026 project hub

Static project page for Smart India Hackathon 2026, problem statement **SIH26052**:
a real-time AI noise-cancellation system for defence radios.

Plain HTML, CSS and JavaScript. No build step, no dependencies, no bundler.

## Layout

```
public/
  index.html          the whole page (styles and script are inline, as in the original)
  images/
    spectrograms.jpg  noisy / enhanced / clean comparison
    signal-chain.jpg  radio -> Raspberry Pi 5 -> headset
```

The demo video is not a file in this repo — it is embedded from YouTube (see
below), so there is nothing to drop in or keep updated on disk.

Everything lives under `public/` because that is the folder Vercel serves as the
site root when no framework is detected — so the deploy needs no configuration.

## Viewing it locally

Open `public/index.html` in a browser. That is all.

If autoplay or the fonts behave oddly from a `file://` URL, serve the folder
over HTTP instead:

```bash
python -m http.server 8080 --directory public
```

## Changing the demo video

The player is a YouTube embed, not a file in this repo. To point it at a
different clip:

1. Upload the video to YouTube (Public or Unlisted — Private videos will not
   play for visitors) and copy its ID: the part of the URL after `/shorts/`
   or after `?v=`.
2. In `public/index.html`, find the `<iframe id="demo" ...>` in the
   "Watch it work" section and replace **both** occurrences of the video ID
   (`WhHAS9xkLww`) — one in the `src` URL, one in the `playlist` parameter
   right after it. The `playlist` copy is what makes YouTube loop a single
   video instead of stopping after one play.

The embed autoplays muted, which is the only way browsers allow autoplay.
The "Tap for sound" button over the bottom-left corner unmutes it via the
YouTube player's own API (turned on by `enablejsapi=1` in the embed URL) —
there is no local video file for it to control.

A landscape recording will show YouTube's own letterboxing inside the
portrait frame; if the replacement clip is landscape, change `aspect-ratio:9/16`
under `.player` in the `<style>` block to `16/9`.

## Replacing the images

Overwrite the files in `public/images/` keeping the same names, or change the
`src` in `index.html` if you use different ones. They are JPEGs (that is what the
originals were); PNG works just as well if you swap the extension in both places.

## Deploying

Push to GitHub, then on vercel.com: **Add New → Project → import this repo →
Deploy**. No settings to change. Every later push to `main` redeploys.
