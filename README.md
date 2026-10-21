# finestworksong.com

Static site for GitHub Pages. No build step.

## Files

- `index.html`: full-screen looping video. Left half links to `/contribute/`, right half to `/film/`.
- `contribute/`: the one-sentence page about sending contributions. "Venmo" links to venmo.com/u/Cooper-Conley.
- `epe/`: unlisted page (no links to it, marked noindex). Steel blue with white text; links to the Drive folder and the Frame.io music video.
- `film/`: the Vimeo embed from the old site.
- `dispatches/`: placeholder for the Substack. Not linked from the homepage right now.
- `better-than-fine-1/`: redirect so the old GoDaddy URL still works.
- `style.css`: shared styles.
- `assets/`: `loop.mp4` (the index-card loop, vertical 1080x1920, 30 seconds, original video quality, audio removed, about 15 MB) and `poster.jpg` (first frame, shown before the video loads and for people who limit motion).
- `fonts/`: Cabin, for the email line.

## Swapping the video

- Keep `loop.mp4` under about 20-25 MB (GitHub's hard limit is 100 MB per file). H.264, no audio track.
- Example: `ffmpeg -i in.mov -an -c:v libx264 -crf 25 -preset slow -pix_fmt yuv420p -movflags +faststart assets/loop.mp4`
- A vertical video gets cropped to a landscape strip on desktop (centered). Keep the important part in the middle third of the frame.

## Deploy

1. Create a GitHub repo (e.g. `finestworksong`) and push these files to your default branch.
2. Repo Settings > Pages > Deploy from branch > your default branch / root.
3. Pages > Custom domain: `finestworksong.com`, then tick Enforce HTTPS once it's available.
4. At GoDaddy (DNS), **before** you cancel the site builder:
   - A records for `@` pointing to `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - CNAME for `www` pointing to `<your-github-username>.github.io`
   - Remove the old A record and any "Website Builder" forwarding.
5. Keep the email records (MX, SPF, DKIM) as they are so `cooper@finestworksong.com` keeps working.
