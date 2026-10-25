# Ink Rider worlds

Portals are objects on a level page. When the rider enters one, the page pauses and the rider plays a
world, then comes back out of the portal's exit and finishes the ride. A world either has its own
tap controls, or is another page you draw on.

## Built

| World | Level | How it plays | Controls |
|---|---|---|---|
| Paper Skies | 5 | The sled becomes a paper plane. Fly through gaps between giant pencils. | Tap to flap |
| Spear Valley | 7 | A second page to draw on. Goblins throw spears on a fixed beat; ink stops spears, so you can draw shields. | Draw, then Ride |
| Doodle Dash | 8 | Off the sled, running along a notebook line. Jump ink blots and erasers, slide under rulers. | Tap right: jump. Hold left: slide |
| Bits & Pieces | 10 | The rider comes apart. Roll as a head in a hat, hop on a one-legged pogo (lean steers your speed even mid-hop; only landing too leaned-over tips you), wobble on two legs with no arms (too fast and the heavy head topples you), run once you get your arms back, and the scarf makes you whole. | Hold to go, let go to ease off |

Daily levels from #2 on put a portal into Paper Skies, Doodle Dash or Bits & Pieces on about 45% of days.

## Ideas

Rough order: most fun for the least new code first.

1. **Lights Out.** The page goes dark except for a small circle of light around the rider. You see the
   whole page for three seconds, then draw from memory. A nod to Memory Draw, this repo's first game.
   *Draw page.*
2. **Gravity Flip.** Tap to flip gravity, so the rider runs on the floor or the ceiling of a corridor of
   staples and paper clips. *Tap.*
3. **The Eraser.** A giant pink eraser chases you across the page and rubs out your lines behind you. You
   draw while you ride, keeping just ahead of it. The first world where you draw in real time. *Draw live.*
4. **Rising Ink.** The page floods with ink from the bottom. Draw short ledges and hop up them before
   the ink catches you. *Draw live.*
5. **Snowball.** Back on the sled, but a snowball rolls behind you and grows with every bump. Keep out of
   its way on a downhill run, then use it to smash a wall at the bottom. *Hold to brake.*
6. **Sticky Swing.** Thumbtacks are pinned across the page. Tap to throw a string to the nearest tack and
   swing; let go to fly. *Hold to grab.*
7. **Origami.** The page folds. Tap a crease to fold the paper over and line up gaps and ledges, then
   ride across. A puzzle world with no time pressure. *Tap creases.*
8. **The Scribble.** Boss fight. A scribble monster throws tangles at you; draw lines to bounce them
   back at it. Three hits and it unravels. *Draw page.*
9. **Inkwell.** Underwater. The sled becomes a tiny submarine that floats unless you hold to dive. Watch
   for currents and blot jellyfish. *Hold to dive.*
10. **Mirror Page.** Everything you draw on the left half also appears flipped on the right half. Two
   riders, one track. *Draw page.*
11. **Desk Top.** Shrink down and ride across a real desk: ruler bridges, crumbs, a rolling pencil, a
   coffee ring that's slippery. *Draw page.*
12. **Sheet Music.** The page becomes a music staff. Jump on the notes in time with the beat. *Tap to
   the rhythm.*

## Adding a world

- **Tap world:** add an entry to `WORLDS` with `name`, `how` and `make(seed, nStars)`. `make` returns an
  object with `press()`, `slide(on)` (or `release()`), `update(dt)`, `status` (`intro`/`ready`/`play`/
  `win`/`fail`), `reason`, `starsGot` and `stars`. Add a `draw…World` function and a branch in
  `drawWorld`, then teach `autopilot` to play it so every layout can be checked.
- **Draw page:** add an entry to `SUBLEVELS` (same format as a level, with `goalPortal: true`) and put a
  portal on a level with `sub: '<id>'`.
- **Checks:** every level, page and world is played by a script before it ships. Pages are ridden with
  a known 3-star route (also used for the Hint button), and worlds are beaten by the autopilot on 300
  random layouts.
