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