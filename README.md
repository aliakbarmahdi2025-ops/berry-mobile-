Build a complete, runnable 3D mobile browser game in this GitHub repository, inspired by the incremental game "Berry Bury Berry" (a surreal first-person incremental game: you grow berries in a strange garden and throw them into an ominous hole for money and upgrades). Do not leave placeholders, stubs, or TODO comments. Every file must be finished and working. Do not copy any assets or text from the original game; use only original, procedural content.

## Tech stack
- Vite + React + TypeScript, three.js via @react-three/fiber and @react-three/drei, zustand (persisted to localStorage)
- No backend and no external assets: build everything from primitive geometry and procedural colors
- Mobile-first (portrait and landscape), 60 fps on mid-range phones: cap pixel ratio at 2, use instancing where useful, avoid expensive shadows

## Core loop (the player is a SEPARATE character from the hole)
- First-person view by default (the player is the gardener). A toggle in settings switches to third-person, where a small 3D gardener model (round body, hat, shovel on the back) is visible.
- The garden contains berry bushes/plants. Berries grow back over time. The player walks up to ripe berries and collects them (auto-pickup within a magnet radius, upgradeable). Collected berries are held in the hand/basket (capacity upgradeable).
- A big ominous hole sits in the garden. It is a separate world object: it slowly drifts and relocates inside a movement range (upgradeable: "Hole Movement Range"), and it grows as it swallows things.
- The player throws berries into the hole with a large Throw button (auto-aim assist toward the hole, with an arc animation). Each berry that lands gives coins. Throwing continuously (hold the button) is allowed, with a throw-rate upgrade.
- Items too big to throw (garden props such as pots, crates, benches, later cars and buildings) can be pushed by walking into them. Pushing a big item into the hole swallows it if the hole is big enough, and swallowing a big item releases a floating star bubble.
- Subtle eerie atmosphere: slightly unsettling music-free ambience via visuals only (fog, low sun, the hole's soft glow, the hole occasionally "breathing"), but keep it friendly and colorful.

## Mobile controls
- Left half: floating virtual joystick (appears at the touch point) for walking, relative to the view direction.
- Right half: touch-and-drag to look around (rotate the camera). A short tap (under 10 px movement) on a star bubble collects it.
- Large Throw button bottom-right. Use pointer events, touch-action: none, safe-area insets, prevent page scroll/zoom.
- Keyboard fallback for desktop: WASD to move, mouse drag or Q/E to look, Space to throw.

## Fruit gnomes
- 7 gnomes with fruit heads: blueberry, apple, kiwi, orange, banana, pineapple, peach. They stand at fixed spots and periodically produce their fruit (cap per gnome) that the player collects and throws. Only the blueberry gnome is unlocked at the start.
- Gnomes are unlocked and upgraded with Stars (level 1 to 8): faster production and higher fruit value.
- Add small "berry buddies": cute sentient berries that wander near the player and, after being bought, automatically collect and throw berries into the hole at a slow rate.

## Currencies
- Coins: earned for every item/fruit that falls into the hole. Spent on character and hole upgrades.
- Stars: released as floating bubbles when big items are swallowed. Tap to collect. Spent on gnome upgrades.

## Upgrade shop (full-screen overlay from a HUD button)
- Coin tab (levels 1 to 10, exponential cost): hole size, hole movement range, walking speed, carry capacity, magnet radius, throw rate, buy berry buddies.
- Star tab: the 7 gnomes (unlock and upgrade).

## Four worlds
1. Small Garden, 2. Neighborhood, 3. Small Town, 4. Big City District.
Each has its own ground/sky colors, arena size, prop set (larger items in later worlds), gnome layout and hole position. Worlds unlock when the hole-size upgrade reaches a threshold. HUD world selector.

## UI and language
- HUD: coins, stars, shop button, world selector, settings (first/third person toggle, reset save).
- All UI text in Persian (RTL), Vazirmatn font with system fallback. Saturated, friendly colors, rounded shapes, soft fog.

## Project requirements
- Structure: src/components (Player, CameraRig, Hole, World, Gnome, BerryBuddy, Bush, Props, Joystick, ThrowButton, Hud, Shop, Settings), src/store, src/data (worlds, fruits, upgrades), src/utils
- All balance constants (costs, rates, sizes, radii) live in src/data
- Add a GitHub Actions workflow that builds and deploys to GitHub Pages (Vite base = repository name)
- Add a Persian README: run locally, deploy, where to tweak balance
- `npm install && npm run build` must pass with no TypeScript or lint errors before finishing
