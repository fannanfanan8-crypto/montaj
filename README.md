# Montaj (مونطاج)

محرر فيديو مجاني كيخدم كامل فالمتصفح. ملف واحد `index.html`، بلا سيرفر، بلا تسجيل، بلا watermark.
الملفات كتبقى فجهازك.

A free video editor that runs entirely in the browser. One file (`index.html`), no server, no account, no watermark.
Your media never leaves your device.

## Features / المميزات

- **Timeline** with five lanes (text, presenter/character, overlay, video, audio): move, trim from either edge, split (`S`), duplicate, delete, snapping, zoom, undo/redo.
- **Text**: Arabic and Latin fonts, outline, shadow, background, pop / slide / fade animations. Drag items directly on the preview.
- **Filters**: looks (cinematic, vintage, B&W…) and brightness, contrast, saturation, blur, sepia, hue. Per-clip speed, volume, fade in/out.
- **Auto-assemble** (tab "تجميع"): drop many clips and get a sequence ordered by natural filename (01, 02, 10), with cross-fades, a unified look, optional title, and **cuts on the beat** of a song or fit-to-music.
- **Scene generator** (tab "توليد"): turn an idea or a script into animated text scenes with gradient backgrounds. Two modes:
  - *Claude* writes the storyboard (only inside the claude.ai artifact, because it uses the artifact `sample` capability).
  - *Local* turns each line of your script into a scene (works everywhere).
- **Presenter** on top of the scenes, three kinds:
  - an animated cartoon character (hair, skin, outfit, glasses, beard; emotions and poses change per scene; mouth moves),
  - your own PNG cut-out,
  - **a real video of you**: circle or rounded bubble, or background removal for a solid-colour background (chroma key, colour sampled from the corners). Scenes are stretched to the length of your video and your own voice is kept.
- **Frame tools**: save the last frame of a clip, or the current frame, as PNG (reference images for image-to-video models).
- **Export** MP4 (when the browser supports it) or WebM, 720p / 1080p, in 9:16, 16:9, 1:1 and 4:5.

## Use it

Open `index.html` in Chrome or Edge. Or serve the folder: `npx serve .`.
Enable GitHub Pages (Settings → Pages → Source: GitHub Actions) and the included workflow publishes it for you.

## Making real AI video clips for free (outside Montaj)

Montaj does not run video models itself. Generate clips elsewhere, then import them and use the **تجميع** tab.

- **Wan 2.2 (TI2V-5B)**: open source (Apache 2.0), text-to-video and image-to-video, 720p at 24 fps, about 5 s per clip. The official repo asks for a 24 GB GPU for TI2V-5B. See the [Wan2.2 repository](https://github.com/Wan-Video/Wan2.2).
- **BytePlus ModelArk (Seedance)**: BytePlus's own blog says each account gets a free token quota for Seedance 1.0 Pro. Check the current quota, expiry and regional rules in your own account, they change.
- To keep one character consistent across clips, use image-to-video with the same reference image, and the "save last frame" button to chain clips. Identity still drifts over long chains.
- Use only your own face and voice, or people who agreed. Do not impersonate anyone.

## Limits

- Export runs in real time and needs the tab open and visible.
- Filters use `CanvasRenderingContext2D.filter` (not available in Safari).
- Projects are not saved between sessions (media files are not stored).
- Chroma key works best with an evenly lit, single-colour background.
- The cartoon character is 2D, half-body, six emotions.
- Browser-only: no AI background removal, no speech-to-text captions yet.

## Develop

```bash
npm install
npx playwright install chromium
npm test            # needs ffmpeg on PATH
```

`index.html` is the source of truth. `python3 scripts/make-artifact.py` writes `dist/montaj.artifact.html`,
the fragment form used when publishing as a claude.ai artifact (the Claude-powered features and the download
capability exist only there).

## License

MIT, see `LICENSE`.
