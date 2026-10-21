# Local Two-Player Prototype Evidence

October 21, 2026. This records a separate design prototype, not shipped production code or a multiplayer network test.

## Implemented in the local preview

- Two concurrent 3D trolley simulations viewed in split-screen on one computer.
- Independent WASD and arrow controls, with separate brake/reverse behavior.
- Identical six-grocery load presets, 100 points each, 3-second countdown and shared 45-second active deadline.
- Real rigid cargo bodies; loss on forbidden-ground contact, deducted once per item.
- Two ordered corner gates, finish delivery-volume check, points-first/time-second ranking and DNF.
- Local pause/focus-loss pause, reset/rematch and narrow-layout adaptation.
- No rival collision; overlapping rivals are visually suppressed near the local cart for readability.

Implementation: Three.js 0.160.1 and cannon-es 0.20.0 loaded from a CDN in the in-conversation preview. Kinematic trolley deck, dynamic groceries, simplified bump. This is neither a validated deterministic Rapier core nor an offline release.

## Checks actually run

Isolated headless system Chrome via Playwright on the development Mac; automated checks, not physical keyboard or human fun measurements.

- Real browser WASD plus arrow keydown events move both players concurrently; an additional P1 turn affects only P1 heading.
- A test fixture drops P1 eggs onto real physics ground: points go 100 -> 80 once, repeated contact keeps 80, P2 stays at 100.
- Pause freezes the simulation tick for both players.
- Stationary competitors both become DNF at tick 2700, exactly 45 active seconds at 60 Hz.
- Scripted controllers completed the spread-out course with both loads intact; 100-point ties resolved to the earlier authoritative finish tick.
- Controlled result fixtures exercise points priority.
- Rematch resets points, timer and active input.
- The browser reported no runtime JavaScript errors in these checks.
- At a 390-pixel outer viewport the preview had no horizontal overflow.

Test-only hooks were added to a separate instrumented copy. The delivered preview has no test hook. These checks do not establish network behavior, production determinism, subjective fun, keyboard rollover compatibility or performance under the intended deployment load.

## Still to validate

Two humans at the actual keyboard; how aggressive/timid driving affects the default stacked load; whether 45 seconds is the right deadline; clarity of losing undelivered airborne cargo at finish. The protected next product gate is human competitive play, followed by the production shared simulation and online authority.
