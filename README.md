# Image Match

Webcam on the left, a matching reaction image on the right. Face and hand tracking run entirely in your browser (MediaPipe Face Landmarker + Hand Landmarker); no video is uploaded anywhere.

## Run it

Easiest: double-click `index.html` to open it in Chrome or Edge, click **Start camera**, and allow camera access.

If the browser refuses the camera on a file opened from disk (Safari and Firefox can), serve the folder locally instead:

```
cd image-match
python3 -m http.server 8000
```

then open http://localhost:8000.

You need an internet connection on first load: the tracking library and models download from jsDelivr and Google's model storage.

## Reactions

| Reaction | Trigger |
|----------|---------|
| neutral  | relaxed face, no hands |
| happy    | smile |
| sad      | frown |
| bleh     | mouth open (tongue out) |
| side     | turn your head to the side |
| up       | tilt your head back, or close your eyes |
| shh      | index finger on your lips |
| thumbs   | thumbs up |
| peace    | peace sign (one hand or two) |
| flex     | raise a fist |
| heart    | heart with both hands |

Hand gestures take priority over facial expressions. The small readout under the camera shows live `yaw` and `pitch` numbers to help tune the head-turn and head-tilt thresholds.

## Use your own images

Click any reaction tile at the bottom and pick an image. It replaces the built-in image for that reaction and is remembered in that browser. "reset" on a tile, or **Reset images** at the top, restores the defaults.

## Tweak it

Everything is in `index.html`:

- `REACTIONS` — the list of reactions (name, default emoji, hint text).
- `T` — sensitivity thresholds. Lower `jawOpen`, `smile` or `frown` to trigger more easily; raise `holdFrames` if the image flickers.
- `classify()` — the rules mapping landmarks to a reaction. Add a new rule there and a matching entry in `REACTIONS`.
