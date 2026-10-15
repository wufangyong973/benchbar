---
title: "Runner gallery"
description: "A look at the built in runners and the example Blob runner, frame by frame, so you can see what a runner does before you draw one."
---

A [runner](runners.md) is the character that sits in the menu bar: a folder
of PNG frames played by state, drawn at 18 points tall. This page shows the
built in runners and the shipped example runner state by state, so you can see
what is possible and how the states differ before you draw your own.

The built in runners, **Bench** and **Coffee cup**, are defined in
[`macos/BenchBar/Runners/BuiltInRunners.swift`](https://github.com/askysh/benchbar/blob/main/macos/BenchBar/Runners/BuiltInRunners.swift).
Their frames are all in one image below.

## Built in runners

![The two built in runners, Bench and Coffee cup, and their running frames](images/runners.png)

Both are template runners: BenchBar paints the alpha in the menu bar's text
color, so they read on a light or dark menu bar. While the bench is up they
loop their running frames (faster when the bench is busy); while it is stopped
they play their sleeping frames slowly.

## The Blob example

[`examples/runners/blob`](https://github.com/askysh/benchbar/tree/main/examples/runners/blob)
is a working custom runner with the script that drew it. Its manifest, next to
the frames it lists:

```json
{
  "name": "Blob",
  "author": "BenchBar example",
  "template": true,
  "states": {
    "running": ["run1.png", "run2.png", "run3.png", "run4.png"],
    "sleeping": ["sleep1.png", "sleep2.png"],
    "crashed": ["wobble1.png", "wobble2.png"],
    "alert": ["alert.png"]
  },
  "frame_order": "forward"
}
```

Its frames per state:

| State | Frames | Plays |
|---|---|---|
| `running` | `run1` `run2` `run3` `run4` | loops; faster when the bench is busy |
| `sleeping` | `sleep1` `sleep2` | loops, slowly |
| `crashed` | `wobble1` `wobble2` | plays 3 times |
| `alert` | `alert` | plays once, holds the last frame |

| | | | |
|---|---|---|---|
| ![running frame 1](images/blob-run1.png) | ![running frame 2](images/blob-run2.png) | ![running frame 3](images/blob-run3.png) | ![running frame 4](images/blob-run4.png) |
| ![sleeping frame 1](images/blob-sleep1.png) | ![sleeping frame 2](images/blob-sleep2.png) | | |
| | | | |
| ![crashed frame 1](images/blob-wobble1.png) | ![crashed frame 2](images/blob-wobble2.png) | | |
| | | | |
| | | ![alert frame](images/blob-alert.png) | |

The Blob is also a template runner (`"template": true`), so BenchBar tints it
in the menu bar's text color; it draws the blob in black on transparent with
details cut out as holes.

## Drawing your own

- Draw at **36 px tall** (18 points at 2x), keep every frame the same size, and
  keep the character in the same spot across frames so it does not jitter.
- A runner that is not a template shows its own colors; a template runner is
  tinted by the menu bar, so details should be cut out as transparent.
- To make frames in code, [`examples/runners/blob/make-frames.swift`](https://github.com/askysh/benchbar/blob/main/examples/runners/blob/make-frames.swift)
  draws the example with Core Graphics:

  ```bash
  cd examples/runners/blob
  swift make-frames.swift
  ```

Full frame rules, the manifest fields, and the import checks are in
[Custom runners](runners.md). The built in names `bench` and `cup` are
reserved; only add art, names, or characters you have the rights to.
