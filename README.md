# Drone Open World

A 3D open-world drone flight simulator that runs in your browser. It started as a PID drone tuner and grew into a sandbox game where the tuning sliders, wind, battery and cargo are all real parts of how the drone flies.

Everything lives in one file: `drone_open_world.html`.

## Running it

1. Open `drone_open_world.html` in a modern browser (Chrome, Edge or Firefox).
2. Click the page or press any key once. Browsers block audio until you do.
3. Fly.

No build step or install. The only external dependency is Three.js r128, loaded from cdnjs, so you need an internet connection the first time. A keyboard or a game controller is required. There is no touch support.

## Controls

### Keyboard

| Key | Action |
| --- | --- |
| W A S D | Tilt: forward, left, back, right |
| Space / Shift | Climb / descend |
| Q / E | Yaw left / right |
| F | Grab or drop the crate |
| C | Cycle camera view |
| R | Respawn at spawn |
| H | Return home |
| L | Headlight |
| V | Acro mode on or off |
| N | Start or cancel the ring race |
| G | Show or hide the goals panel |
| M | Sound on or off |
| Tab | Tuning panel |

### Controller

Standard gamepad layout. Plug it in and press any button so the browser detects it.

| Input | Action |
| --- | --- |
| Left stick | Climb and yaw |
| Right stick | Tilt |
| Triggers (RT / LT) | Extra climb / descend |
| X | Grab or drop the crate |
| Y | Cycle camera view |
| A | Respawn |
| B | Return home |
| LB | Headlight |
| RB | Acro mode on or off |
| Back | Start or cancel the ring race |
| Start | Tuning panel |

## Flight modes

- **Stabilized** (default): the sticks set a tilt angle and the drone levels itself when you let go.
- **Acro**: the sticks set rotation speed and the drone does not self-level. This is how you do flips, barrel rolls and side flips. Turn **Altitude hold** off for the best results, since altitude hold fights you when the drone is upside down.
- **Altitude hold on**: a PID loop holds your height. **Off**: manual throttle, where stick centered is roughly hover.
- **Return home**: the drone climbs to about 25 m, turns, flies back and lands. Moving a stick cancels it. It also triggers automatically at low battery, which you can turn off.

Turn banking and input smoothing make the motion feel less robotic. Both have sliders.

## The HUD

Height above ground, speed, battery and thrust, plus gates, deliveries and crashes. It also shows the current objective with a direction arrow, flight mode, camera view, distance from home, flight time and battery voltage (4S pack). A small graph plots altitude against the target height, which is useful when tuning.

## Cameras

Pick one in the tuning panel or cycle with C or Y:

- **Chase**: follows behind, pulls back and widens the field of view with speed, and tilts with the drone.
- **FPV**: first person from the drone.
- **Orbit**: drag to rotate, scroll to zoom.
- **Cinematic**: a slow drifting camera.
- **Pilot at home**: you stand at the home pad and watch the drone, with zoom as it flies away.
- **Top-down**: heading-up view from above.

## Tuning panel

Open with Tab, Start, or the **Tuning panel** button.

- **Tuning**: altitude P, I, D and tilt P, D, plus presets (P only, P + D, P + I + D). Also mystery cargo, wind gusts, motor lag, battery sag and sensor noise, and kick buttons to shove the drone.
- **Sound**: master, motor, wind and effects volume.
- **World look**: time of day, from day through dusk to night.
- **Flight feel**: Cine, Normal and Sport presets, max tilt angle, speed limit, climb rate, yaw rate, motor power, air drag, battery life, turn banking and input smoothing.
- **Controls and camera**: stick expo and deadzone, field of view, FPV camera tilt, camera dynamics, chase distance, invert pitch, headlight, auto return home.

## What P, I and D do

- **P** pushes in proportion to the error. Too little is sluggish, too much overshoots and bounces.
- **I** builds up over time to cancel steady errors like heavy cargo or a weak battery. Too much makes it swing slowly.
- **D** brakes based on how fast the error is changing. It damps wobble and overshoot. Too much gets jittery, especially with sensor noise on.

Try the **P only** preset to see it oscillate, then add D to settle it, then add cargo and I to see the height hold recover.

## The world

A 580 m open map with hills, lakes, around 380 trees, a small village near spawn, towers with beacons and 14 rings to fly through. Day, dusk and night each have their own sky, clouds and stars. You cannot fly below the water.

## Goals and scoring

- **Crate delivery**: a pink beam marks the crate and a green beam marks the delivery pad. Grab the crate low and slow (it adds 25% weight), fly to the pad and drop it. Faster and more precise deliveries score more.
- **Rings**: every ring you fly through scores points.
- **Ring race**: a fixed 6-ring time trial. The clock starts when you pass the first ring. A gold marker shows the next ring and your best time is saved.
- **Goals list**: 13 goals covering rings, deliveries, altitude, speed, flips (Acro only), low passes, distance, endurance and the race. Each pays a bonus when completed.
- **Battery**: it drains in flight and recharges when you land on the home pad or a delivery pad. At 0% the drone respawns at spawn after a moment.
- **Crashes**: hard hits on the ground, trees, towers and houses count as crashes.

Completed goals, your best race time and your high score are saved in your browser's local storage.

## Sound

All sound is synthesized in the browser. There are no audio files: motor hum that follows thrust, wind rush that follows speed, and effects for rings, crashes, grabbing, deliveries and respawns.

## Known limits

- The flight model tracks roll and pitch as simple angles. Clean single-axis flips and rolls work well, but combined rotations and vertical pitch are approximate.
- The flip counter is rough, so a messy tumble in Acro can count.
- The world is generated from a fixed seed, so it looks the same every time.
- Keyboard or controller only.

## Credits

Built up from `PID_drone_tuner_3D.html`, keeping its altitude PID, tilt control, motor lag, battery sag, cargo and wind mechanics.
