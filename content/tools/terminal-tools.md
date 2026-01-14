---
title: Simple tools to use in the terminal
created: 2026-01-14
tags:
  - tools
---
## Make a gif from a video

```bash
ffmpeg -i movie.mov -vf "scale=iw/3:ih/3" -pix_fmt rgb8 -r 15 output.gif && gifsicle -O3 output.gif -o output.gif
```

## Mov to mp4

```bash
ffmpeg -i movie.mov -vf "scale=iw/2:ih/2" -vcodec libx264 -crf 28 -preset medium -acodec aac -b:a 128k output.mp4
```