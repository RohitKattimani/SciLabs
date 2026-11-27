# SciLab

Interactive science simulations that run in the browser. Drag a pendulum, heat a gas, launch a planet, and watch what happens.

SciLab has 38 hands-on experiments across six subjects. Every experiment starts running straight away, has sliders you can also type numbers into, shows live readouts, and comes with a short prompt to get you asking why.

## Experiments

**Physics (14)**
Cannon Range, Pendulum Playground, Wave Rope, Ramp Slide, Spring Bounce, Cart Collisions, Light Bender, Standing Waves, Beat Frequencies, Motion Graphs, Lens Image Finder, Damped Oscillator, Glowing Heat, Photoelectric Switch

**Chemistry (6)**
Gas Chamber, pH Mixer, Decay Clock, Gas Law Curves, Titration Curve, Cooling Cup

**Astronomy (7)**
Orbit Lab, Moon Phases, Solar System Clock, Kepler Orbits, Exoplanet Transit, Why We Have Seasons, Jump on Planets

**Biology (5)**
Bunny Evolution, Population Growth, Predator and Prey, Gene Pool, Enzyme Speed

**Math (4)**
Curve Dancer, Wave Builder, Bell Curve, Sine Explorer

**Electricity (2)**
Ohm's Loop, Capacitor Charge

## Features

- Live animation with play and pause on every experiment
- Sliders paired with number fields, so you can drag or type an exact value
- Direct manipulation where it makes sense, such as dragging the pendulum bob or pulling the spring
- Live readouts that update as you change settings
- A "try this" prompt on every experiment
- Searchable, filterable catalog with a distinct thumbnail for each experiment
- Works on desktop, tablet and phone
- Light and dark themes that follow the system setting
- Respects reduced-motion preferences

## Project structure

```
index.html   Landing page with a live double pendulum demo
app.html     The simulation library (catalog plus all experiments)
vercel.json  Clean URL setting
```

There is no build step, no framework and no dependencies. Both pages are single files of plain HTML, CSS and JavaScript, drawn with the Canvas 2D API. The only external resource is the Google Fonts stylesheet (Bricolage Grotesque and Figtree).

## How the experiments are built

Every experiment is a small object that describes itself:

```js
{
  id: 'pendulum',
  name: 'Pendulum Playground',
  sub: 'Physics',
  desc: 'Drag the bob, then let go.',
  try: 'Drag the bob to a small angle and note the period.',
  ctl: [{ k: 'L', l: 'String length', min: .4, max: 2, v: 1.2, u: ' m', st: .05 }],
  init: () => ({ th: .9, w: 0 }),
  step(s, c, dt) { /* advance the physics */ },
  draw(g, w, h, s, c, C) { /* paint one frame */ },
  read: [['Period', (s, c) => /* formatted value */]]
}
```

A shared runtime turns that description into the page: it builds the sliders and number fields, runs the animation loop, wires up pause and reset, handles pointer dragging, and refreshes the readouts every frame.

There are two kinds of experiment:

- **Animated simulations** step real physics each frame. Examples are orbits, collisions, gas particles, the double pendulum and natural selection.
- **Graph experiments** share one plotting engine. Each defines its curves as functions of the sliders, and a moving marker sweeps along them. Their catalog thumbnails are generated from the experiment's own curve.

## Author

Rohit Kattimani

© Rohit Kattimani, 2026
