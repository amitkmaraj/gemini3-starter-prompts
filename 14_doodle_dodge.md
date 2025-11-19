# Prompt: Doodle Dodge - The Hand-Drawn Endless Runner

**Goal:** Build a fully functional, polished, endless runner game called "Doodle Dodge" using React, TypeScript, Tailwind CSS, and the HTML5 Canvas API, featuring a unique "Hand-Drawn Notebook" aesthetic.

**Prompt:**
> "Act as a world-class Senior Creative Frontend Engineer and Game Developer. I want you to build a fully functional, polished, endless runner game called 'Doodle Dodge' using React, TypeScript, Tailwind CSS, and the HTML5 Canvas API.
>
> **The Aesthetic: Hand-Drawn Notebook**
> *   **Background:** A scrolling notebook paper effect (white/cream background with faint blue horizontal lines and a vertical red margin line).
> *   **No Images:** All graphics (player, obstacles, UI) must be drawn *procedurally* using Canvas paths.
> *   **Style:** Implement a `drawSketchyLine` helper that draws lines twice with slight random jitter to simulate a hand-drawn ink look. Implement `drawSketchyCircle` for imperfect, wobbly circles.
> *   **Animations:** The player (Stickman) should have procedural limb animations (sin/cos waves) for running and a specific 'tuck' animation for jumping.
> *   **The Pencil Mechanic:** Obstacles should not just 'pop' in. A giant floating pencil should fly in, 'draw' the obstacle rapidly, and then the obstacle becomes physical.
>
> **Core Mechanics:**
> *   **Lanes:** 3 horizontal lanes. Player runs on left, obstacles come from right.
> *   **Controls:** Up/Down (Switch Lanes), Space/Right (Jump with Pseudo-3D parabola), Enter (Shoot).
> *   **3-Axis Collision:**
>     *   *Lane (Z):* Must be in same lane.
>     *   *Horizontal (X):* Standard overlap.
>     *   *Altitude (Y):* Track player height. Ground obstacles (Rocks) hit low feet; Flying obstacles (Paper Planes) hit high body; Holes are safe if jumping.
> *   **Scoring:** Distance + Destruction Bonus.
>
> **Game Content:**
> *   **Player:** Stickman with hearts.
> *   **Obstacles:** Rock/Spike, Hole, Paper Plane, Ruler (blocks lane), Eraser (moving).
> *   **Power-Ups:** Machine Gun, Shield, Eraser Bomb (wipe screen), Health Heart, Speed Boost/Slow Mo.
>
> **Technical Architecture:**
> *   **Game Loop:** Use `requestAnimationFrame` inside a `useEffect`.
> *   **State Management:** Use `useRef` for ALL mutable game state (positions, arrays, particles) to ensure 60 FPS without React re-renders. React State only for HUD (Score, Menu).
> *   **Files:** `GameCanvas.tsx` (Engine), `drawing.ts` (Sketchy utils), `types.ts` (Interfaces), `App.tsx` (UI).
>
> **Polish ('Juice'):**
> *   **Particles:** Sketchy bursts on destruction.
> *   **Screen Shake:** On impact/bomb.
> *   **Parallax:** Background grid moves slower than foreground.
> *   **Combos:** 'Near Miss' bonus points.
>
> Please generate the complete code for this application, ensuring all files are linked and the game is playable immediately."
