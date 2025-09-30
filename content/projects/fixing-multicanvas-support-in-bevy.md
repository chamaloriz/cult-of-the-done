---
title: Tried fixing multicanvas support in bevy
created: 2025-09-30
tags:
  - bevy
  - in-progress
---

I was working on using bevy for drawing multiple graphs on a web page using WASM and wanted to populate two canvas elements on a webpage.

```bash
panicked at /Users/kelp/.cargo/registry/src/index.crates.io-1949cf8c6b5b557f/bevy_render-0.16.0/src/view/window/mod.rs:338:51:
No supported formats for surface

Uncaught RuntimeError: unreachable
```

I first tried to see where the bug is coming from by using bevy from my local folder using :

```rust
[dependencies]
my_lib = { path = "../my_lib" }
```

after logging the code around the issue I did not really understand the issue since I'm still a bit new to the bevy / wgpu ecosystem. But to be sure that the issue was not coming from the underlying wgpu I tried to find evidence that drawing to multiple canvases was possible and found [this post](https://github.com/gfx-rs/wgpu/discussions/4177) confirming that it was indeed possible.

my hypothesis is that bevy does not create the second surface in time for the rendering, still investigating, check out the status on [this issue]( https://github.com/bevyengine/bevy/issues/20453).