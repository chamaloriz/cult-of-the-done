---
title: My first rust crate "bevy_split_canvas"
created: 2026-01-07
tags:
  - success
  - bevy
  - wasm
---
# I published [my first crate on crates.io](https://github.com/chamaloriz/bevy_split_canvas).

After finding out that it's not currently possible to render to multiple canvases in bevy "[[fixing-multicanvas-support-in-bevy]]". I created `bevy_split_canvas` it takes screenshots of the main canvas and splits it via the cameras.

![[bevy-split-canvas-demo.gif]]

## Unexpected find

![[bevi-crate-discovery.png]]

I also discovered that Bevy didn't reserve the misspelled "[bevi](https://github.com/bevyengine/bevy-crate-reservations/commit/5336f19134d34fb4349e9eb056c31ea081322748)" crate, I'm glad that I was the first to find this out, as crates are first-come, first-served.

Also, [Cart](https://github.com/cart) has a point with the following:

![[cratesio-should-support-namespacing.png]]
