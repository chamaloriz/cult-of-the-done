---
title: Multicanvas support in bevy
created: 2025-09-30
updated: 2025-12-20
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

---

## The conclusion

*Written on the 20th of December 2025, whereas the issue was created on the 7th of August.*

After trying to solve this issue I discovered that it's a known limitation of WebGL, bevy only creates a single `wgpu::Instance` but for it to work you would need to create a `wgpu::Instance` per html canvas.

An alternative solution would be to just create a single canvas but to split it's contents to multiple-canvases something like that :

```js
const canvas = document.getElementById('canvas');
const canvas1 = document.getElementById('canvas1');

const ctx1 = canvas1.getContext('2d'); 

requestAnimationFrame(() => { 
	canvas1.width = canvas.width;
	canvas1.height = canvas.height; 
	ctx1.drawImage(canvas, 0, 0); 
});
```