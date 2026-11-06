# Plumb: hang pictures centered, by voice

Plumb is a single-page web app. You prop your phone up facing the wall, hold the picture up, and the phone tells you where to move it ("Left, about 3 inches… a touch down… raise the right side"), then beeps faster as you get closer. Once the picture is centered it tells you where to put the nail.

**Live app:** https://andersondaniel48-dot.github.io/pictureframing/

## How to use it

1. Stick a small, **brightly colored marker** on each **top corner** of the frame (dot stickers, sticky-note squares or painter's tape). Pick a color that doesn't show up anywhere else on the wall.
2. Open the app on your phone, tap **Start camera**, and prop the phone 6–10 ft from the wall with the back camera facing it. Use the level readout to get it straight.
3. Enter the frame's width and height, the hanger type, and how far the hanger sits below the top of the frame.
4. Choose what to line it up with:
   - **Center over an item:** tap the top-left and top-right corners of the sofa, bed or dresser, then set the gap above it.
   - **At a height:** tap where the wall meets the floor, then set the height (57 in to center by default) and whether it's measured to the picture's center, top or bottom. You can also tap two points (wall corners, a door edge) to center between them.
5. Pick up the picture and tap one of the markers on screen so the app learns its color. Then follow the voice.
6. When it says "Got it", make a pencil mark at the top center of the frame. The app tells you how far below that mark the nail (or two nails, for D-rings) goes.

## How it works

- **Tracking:** each camera frame is shrunk to about 90k pixels and checked for the marker's color (in HSV). The matching pixels are split into two clusters, which gives the two top corners of the frame. Their midpoint is the frame's top center, and the angle between them is the tilt.
- **Scale:** the pixel distance between the markers divided by the frame width gives pixels per inch. Since the frame is flat against the wall, that same scale measures the gap above the sofa or the height from the floor.
- **Guidance:** it gives one correction at a time, in order: side to side, then up and down, then level. Left and right are from your side, since you and the back camera face the same way. You're "on" within ½ in and 0.75°, and it locks after you hold still for about 1.3 s.
- **Voice and sound:** voice uses the browser's built-in speech (`speechSynthesis`) and the beeps use Web Audio. The screen is kept awake with the Wake Lock API where it's supported.

Everything runs on the phone. No video leaves the device.

## Tips

- Put the phone at roughly the height the picture will hang, and hold the frame by its sides or bottom so your head doesn't block the markers.
- The more square the phone is to the wall, the more accurate the measurements.
- If tracking jumps around, tap **Show what I see** to check which pixels match the marker color, and tap **Re-pick color** if needed.

## Running locally

It's one file, `index.html`. Browsers only allow camera access over `https` or on `localhost`. To test on a phone, use the GitHub Pages link above.
