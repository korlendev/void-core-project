# VOIDCORE
## ROOM-BY-ROOM SURVIVAL ROGUELITE
*PROJECT BIBLE & PRODUCTION PLAN · v1.0*

> Enter the room. Build the loadout. Survive the run.

## Core pitch
VOIDCORE is a 2D top-down room-based survival roguelite. Each encounter is one room and one wave. A floor is a connected room graph; players clear a room, choose a route, draft an upgrade and continue. Melee is the primary combat layer, firearms are secondary ranged tools, and magic abilities provide control, defense and burst windows.

## Non-negotiable design decisions
- Single-player and offline-first.
- One room encounter = one wave. No confusing nested wave numbering in the first version.
- One floor map contains 6 rooms for the first vertical slice; later zones can use 8–10 rooms.
- Always-visible in-room minimap plus a larger route-map overlay between rooms.
- Melee-first combat; firearm support; magic utility/control.
- Build with existing pixel-art packs; do not require bespoke character or environment art to prototype.

## 01 · PRODUCT IDENTITY
### Product summary
VOIDCORE is a 2D top-down room-based survival roguelite. The player fights through a connected map of combat rooms, clearing one encounter per room, choosing routes, collecting rewards and building a run-specific loadout. The combat identity is deliberately layered: melee is the main damage source, firearms provide reliable ranged pressure, and magical abilities control space, protect the player or create burst windows.

### Design pillars
- **Room-by-room clarity:** Every encounter occupies one distinct room. The player always knows the current room, the objective, the exit condition and the next route.
- **Melee-first combat:** Close-range weapons define the rhythm and most builds. Firearms support, interrupt or finish targets; magic creates tactical opportunities rather than replacing the weapon loop.
- **Readable arena UI:** Health, weapon readiness, cooldowns, objectives and a useful minimap remain visible without covering the action.
- **Roguelite variety:** Room choices, three-option rewards, weapon synergies and changing enemy mixes create different runs from a compact content set.
- **Asset-efficient production:** Use one coherent pixel-art pack or modular tileset family. Reuse room modules, enemy silhouettes, VFX palettes and UI components rather than inventing hundreds of unique assets.

### Target experience
A focused solo game for short, replayable runs. The first playable target is a single zone with six rooms, one miniboss/boss encounter, three enemy archetypes, one melee weapon family, one firearm and two magical skills. The larger design expands only after that slice feels good.

## 02 · GENRE, PLATFORM & SCOPE
### Genre and camera
2D top-down action roguelite / arena survival. The camera follows the player with soft dead-zone smoothing. Rooms are discrete arenas connected through a node-based floor map. No open-world streaming is required.

### Platforms
Primary development target: Windows desktop in a browser or packaged desktop build. Architecture should remain touch-friendly so Android can be considered later. Initial design assumes solo offline play; online services are not required.

### Session length
Target 12–20 minutes for a complete early-game run, with individual rooms generally lasting 35–75 seconds plus reward/route selection.

### Scope guardrails
- **In scope for first playable:** One playable Hunter-style combatant, one zone, six rooms, room map, minimap, melee, one firearm, two magic skills, three regular enemies, one elite variant, one boss, three-choice room rewards, pause and local save.
- **Not in first playable:** Online co-op, PvP, procedural infinite world, crafting trees, dozens of characters, cinematic story campaign, mod support, cloud saves.
- **Content expansion rule:** Add a new enemy, weapon or room only when it introduces a clear new decision. Prefer remixing enemy combinations and room geometry over adding many near-identical assets.

## 03 · CORE GAME LOOP
### Run flow
Main Menu → Character / Loadout selection → Zone Map → Enter Room (Encounter = Wave) → Clear objective → Reward choice → Return to Map → Choose connected room → Elite / Boss → Zone clear → Results.

### The one-room-one-wave rule
A room encounter is the unit of progression. Room 01 is Wave 01, Room 02 is Wave 02, and so on. A room may spawn several timed enemy groups, but it remains one encounter and has one clear condition. The HUD should label both together, for example: WAVE 03 · ROOM 03 / 08.

### Room completion
A standard combat room clears when all required enemies have been defeated. A survival room clears when the timer reaches zero and the player is alive. An objective room clears when its target is completed. Once clear, the combat director stops spawning enemies, reward UI appears and the room exit becomes active.

### Between-room decisions
The player sees the floor map and may choose from unlocked connected rooms. Room types communicate risk and reward before entry: Combat, Cache, Forge, Elite, Event or Boss. At least one valid route must always remain to the boss.

## 04 · FLOOR MAP, ROOMS & MINIMAP
### Map structure
A zone is a connected graph of 6–10 rooms. The initial vertical slice uses one 6-room route with one branch. The expanded format uses 8 rooms per zone: Entrance, Combat, Branch Choice, Cache/Event, Combat, Forge/Rest, Elite, Boss. Each room is loaded as a separate arena scene; the map graph persists across room transitions.

### Room categories
- **Combat:** Standard enemy mix; predictable difficulty; standard reward.
- **Ambush:** Enemies enter from multiple spawn gates; short setup warning before combat.
- **Cache:** No mandatory combat; choose one reward from a small cache or accept a trade-off.
- **Forge / Rest:** Repair health/guard, upgrade a weapon or reroll one reward at a cost.
- **Elite:** A tougher enemy composition with one affix; better reward.
- **Boss:** A unique multi-phase encounter; completing it ends the zone.

### Minimap - in-room
A compact top-right panel shows the current room outline, walls/obstacles, player marker, exit, objective marker and important pickups. Enemy markers should be shown only when revealed or within a short detection radius to avoid turning the minimap into wall-hack information. A toggle can enlarge the map.

### Floor route map
After clearing a room, show the node map overlay. Nodes use distinct shapes and colors: current = bright cyan ring, cleared = filled teal, available = amber outline, locked = muted slate, cache = gold chest mark, elite = violet/red mark, boss = red crown/skull-like abstract mark. Lines show legal connections. The selected next room displays its type, threat and reward preview.

### Room layout rules
- **Combat space:** One readable central arena with at least two movement lanes and a safe route around major obstacles.
- **Spawn fairness:** Never spawn an enemy directly on the player. Show a brief spawn marker before dangerous entries.
- **Exit placement:** Exit should be visible and reachable. It activates only after the encounter clear condition is met.
- **Camera:** Keep the player and high-priority threats inside the central safe area. Avoid camera shake that hides the minimap or HUD.

## 05 · COMBAT DESIGN
### Combat hierarchy
Melee is primary. Firearms are secondary ranged tools. Magic abilities provide control, defense, mobility or burst damage. The three layers should have separate purposes so that carrying a gun does not make melee irrelevant.

### Melee - primary
The default attack is a directional arc or short combo around the player. Weapon families can include blade, hammer, spear and twin short blades. Each family changes reach, recovery, stagger and hit pattern. Melee hits reward positioning and timing. Avoid realistic weapon handling detail; all combat is stylized fantasy action.

### Firearms - secondary
One firearm slot supports safe ranged pressure and finishing low-health enemies. Use abstract, fictional weapons such as Pulse Pistol, Arc Carbine or Scatter Emitter. The player manages a small magazine and reload/cooldown window. Firearms should have lower sustained damage than a well-executed melee build, but better reach.

### Magic - tactical
Two ability slots. Example skill roles: Arc Burst (short-range burst), Gravity Well (gathers enemies), Ward (temporary damage reduction), Blink (short reposition) and Sigil Mine (delayed area control). Each uses energy or cooldown. Magic should solve situations, not replace all weapon attacks.

### Recommended PC controls
- **Move:** WASD
- **Aim:** Mouse
- **Melee:** Left Mouse / hold for repeat attack if the equipped weapon supports it
- **Firearm:** Right Mouse or a configurable key
- **Magic skills:** Q and E
- **Dodge:** Space
- **Reload / weapon utility:** R
- **Room map:** Tab
- **Pause:** Esc

### Mobile control plan
If Android is added later: left virtual stick for movement; right-side attack area for melee; separate firearm and two skill buttons; dodge as a dedicated button. All buttons must have configurable size/opacity and safe-area padding.

### Combat readability
Use clear telegraphs: enemy wind-up ring, melee arc flash, projectile trail, boss attack lane and hit feedback. Use hit-stop sparingly, short screen shake only for heavy hits, and colorblind-safe shape cues rather than color alone.

## 06 · WEAPONS, SKILLS & BUILDS
### Equipment slots
MVP loadout: one melee weapon, one firearm and two magic skills. Full target: two melee options to swap between, one firearm, two magic skills and up to four passive relics. Keep early inventories small so the player understands each choice.

### Melee families
- **Blade:** Fast, medium reach, reliable combo; balanced starter.
- **Hammer:** Slow, wide impact, high stagger; rewards commitment.
- **Spear:** Long narrow thrust; spacing and line control.
- **Twin blades:** Rapid short arcs; strong against nearby groups but low reach.

### Firearm families
- **Pulse Pistol:** Reliable single shots; starter sidearm.
- **Arc Carbine:** Short burst; good for mid-range pressure.
- **Scatter Emitter:** Wide spread at close-to-mid range; limited magazine.

### Magic roles
- **Arc Burst:** Quick damage pulse around the player.
- **Gravity Well:** Pulls light enemies toward a point.
- **Ward:** Temporary defensive barrier.
- **Blink:** Short dash with a brief safety window.
- **Sigil Mine:** Delayed area effect that rewards room positioning.

### Upgrade draft
After each combat room, present three upgrade cards and let the player select one. Cards are categorized as Weapon, Firearm, Arcana, Defense, Mobility or Economy. Examples: +melee reach, faster combo recovery, firearm reload speed, larger ward radius, dodge cooldown reduction or extra cache currency. Every card must state the exact stat it changes and its rarity.

### Build synergies
Offer simple tags: Edge (melee), Ballistic (firearm), Arcane (magic), Guard (defense), Momentum (movement). A build becomes interesting when two tags interact, e.g. melee hits restore a little arc energy or defeating an enemy during a Ward window briefly improves melee stagger. Keep synergy text explicit and testable.

## 07 · ENEMIES, BOSSES & DIRECTOR
### Enemy archetypes
- **Chaser:** Moves toward the player and pressures close-range positioning.
- **Skirmisher:** Circles the player and attacks after a short tell.
- **Ranged Caster:** Fires slow, readable projectiles from a distance.
- **Brute:** Slow, high-health unit with a clearly telegraphed charge.
- **Controller:** Places a temporary hazard zone or summons a minor threat.

### Elite modifiers
Use a small pool of readable modifiers: Swift (faster movement), Armored (reduced frontal damage), Volatile (leaves a brief hazard when defeated), and Siphon (briefly strengthens nearby enemies). Do not stack more than one modifier in early rooms.

### Boss design
A boss should have 2–3 distinct phases, each with a telegraphed pattern and recovery window. First boss prototype: Core Sentinel - a large construct guarding the zone exit. The boss must remain readable in a crowded arena and should not rely on unavoidable damage.

### Encounter director
Each room has a budget of threat points. The director spends that budget on enemy types and spawn timings. The budget increases by room index and zone. Add a short warning before elite/boss spawns. Cap simultaneous enemies for performance and readability.

## 08 · REWARDS, PROGRESSION & DIFFICULTY
### Reward cadence
Standard room clear: choose one of three upgrade cards or take a small currency bundle. Cache room: choose one of two rewards. Forge: heal, improve one item or reroll a card. Elite: guaranteed higher rarity. Boss: major relic and next-zone unlock.

### Run currency
Use one run currency, provisionally Shards, for shops and rerolls. Keep permanent meta progression separate and optional. The first prototype can omit meta progression; focus on run balance first.

### Player stats
Core stats: Max HP, Guard, Move Speed, Melee Power, Melee Speed, Melee Reach, Firearm Power, Reload Speed, Arc Power, Arc Energy and Pickup Range. Only surface the most relevant changes in a compact inspect panel.

### Difficulty curve
Increase room threat through enemy mix, spawn pressure and arena constraints, not simply by inflating enemy health. Add one new decision or enemy behavior at a time. Boss room difficulty should come from patterns and spacing, not unreadable projectile density.

### Death and restart
A run ends when HP reaches zero. Results show rooms cleared, enemies defeated, build tags, best time and earned unlock progress. Restart should be immediate and preserve permanent settings/unlocks.

## 09 · UI / UX SYSTEM
### Visual direction
Premium dark action-game HUD with graphite panels, subtle glass-like layers, cool cyan highlights, amber reward accents and violet arcana accents. Use crisp pixel sprites in the game world, but keep HUD typography clean and highly legible. Avoid excessive glow and tiny text.

### HUD layout
- **Top-left:** Health, guard/armor, XP or room reward progress; compact numeric values and readable bars.
- **Top-center:** Zone name, WAVE/ROOM index, encounter objective and optional timer.
- **Top-right:** Persistent minimap panel; small room layout with player, exit and discovered threats/objectives. Expand with Tab.
- **Bottom-center:** Melee weapon, firearm ammo/reload, two magic abilities with cooldown rings and dodge cooldown.
- **Bottom-left:** Run currency and short pickup notifications.
- **Right edge:** Boss bar when a boss is active; otherwise room modifiers/objective hints.

### Screens
- **Main Menu:** Continue / New Run / Collection / Settings / Credits. Use a live animated arena background but keep the action behind the menu low contrast.
- **Character & Loadout:** Character portrait, passive trait, melee slot, firearm slot, two arcana slots and starting stats.
- **Floor Map:** Room node graph, current room, available routes, threat/reward preview.
- **Reward Draft:** Three large cards with icon, rarity, category, exact stat change and one-sentence description.
- **Inventory / Collection:** Weapons, arcana, relics and discovered enemies; filters by category.
- **Pause:** Resume, controls, settings, abandon run.
- **Results:** Run summary, room path, build, rewards and retry.

### Interaction rules
All important buttons should have hover, focus, pressed and disabled states. Support keyboard navigation. Reward cards must be selectable by mouse, keyboard and touch. Keep hit targets large enough for later mobile support. Minimap markers must include shape/icon differences, not color alone.

## 10 · ART DIRECTION & ASSET SPEC
### Pixel-art target
Recommended baseline: 32×32 world tiles, characters around 32×48 or 48×48 depending on the chosen pack, enemies from 32×32 to 64×64. This is a target, not a demand to resize every asset; choose one coherent pack and preserve native pixel scale.

### Palette
World: deep graphite, muted steel, desaturated teal. Gameplay cues: cyan for player/usable objects, amber for rewards, violet for arcana, red-orange for danger. Use a restrained palette so attacks and objectives stand out.

### Player sprite states
Idle, walk (4 or 8 directions), melee attack, firearm aim/fire, cast, dodge, hurt, defeat. For the first slice, prioritize idle, 4-direction walk, melee attack, hurt and dodge.

### Enemy sprite states
Idle, move, telegraph/attack, hurt, defeat. Boss needs a distinct silhouette and 2–3 attack tell animations.

### Environment set
Modular room floor, wall, corners, doors, pillars, crates, barriers, hazards, spawn gates, exit portal and decorative props. Prefer tileset autotiling or reusable room chunks.

### VFX set
Melee slash arc, hit spark, projectile trail, impact, magic circle, gravity field, ward barrier, dodge afterimage, spawn telegraph, boss warning and room-clear effect.

### UI asset set
Weapon icons, magic icons, enemy icons, room-node markers, minimap legend, card rarity frames, health/guard/energy icons, cursor states and controller hints.

### Asset sourcing
Search for complete top-down arena/roguelite packs first. Check sprite scale, animation frame count, direction count, commercial-use license, modification rights and attribution rules before mixing packs.

## 11 · SOUND & ACCESSIBILITY
### Sound categories
Melee swing/hit, firearm shot/reload, magic cast/impact, enemy alert/attack, pickup, reward choice, room clear, boss warning, UI hover/confirm, ambient zone loop and boss music.

### Mixing
Separate sliders for Master, Music, SFX and UI. Keep critical telegraph sounds distinguishable from ambient effects. Add visual telegraph equivalents so sound is never the only warning.

### Accessibility
Remappable keyboard controls, adjustable screen shake, reduced flashes, colorblind-safe markers, scalable HUD, pause-anytime in solo play and optional aim assist. Avoid rapid full-screen flashes.

## 12 · TECHNICAL ARCHITECTURE
### Recommended stack
Vite + TypeScript + Phaser for the 2D game runtime. React can be used for menus, inventory and settings UI as an overlay; Phaser owns the real-time world, collisions, combat timing and scene transitions. Tiled can author room geometry; store room graph and spawn data in JSON.

### Scene structure
- **BootScene:** Load minimum boot assets and global config.
- **PreloadScene:** Load selected zone pack and shared combat assets.
- **MenuScene:** Main menu / character selection entry.
- **MapScene:** Floor route graph and room choice.
- **RoomScene:** Player, enemy, collision, spawn director and room objective.
- **UIScene:** HUD, minimap, reward draft and pause overlay.
- **ResultsScene:** Run summary and retry/return.

### Systems
- **RunState:** Current zone, room node, resources, selected loadout, upgrades and random seed.
- **RoomGraph:** Valid connections, node type, visited/cleared/locked state.
- **EncounterDirector:** Spawn schedule, threat budget, room clear condition.
- **CombatSystem:** Hitboxes, attack windows, damage, stagger, invulnerability frames and status effects.
- **WeaponSystem:** Melee combo state, firearm magazine/reload and weapon cooldowns.
- **ArcanaSystem:** Skill cooldown/energy, area effects and status effects.
- **MinimapSystem:** Current room geometry, player marker, exit, objectives and discovered threats.
- **RewardSystem:** Three-card draft, rarity weighting and synergy tags.
- **SaveService:** Settings, unlocks and run checkpoint/summary using local storage or IndexedDB.

### Data-driven content
Enemies, weapons, skills, upgrades, rooms and zones should be configured in typed data files (JSON/TS objects) rather than hard-coded inside scene classes. Keep balance values easy to tune.

### Performance
Target a stable 60 FPS on modest PCs. Use object pools for projectiles and hit effects, cap simultaneous enemies and particles, and avoid rendering hidden room content. Pixel art should use nearest-neighbor scaling.

## 13 · DEVELOPMENT ROADMAP
### Milestone 0 - Project foundation
Set up Vite, TypeScript, Phaser, lint/build scripts, asset loader, resolution scaling and input abstraction. Exit: blank game scene renders at target resolution and resizes cleanly.

### Milestone 1 - Room prototype
Create one room, player movement, collision, camera and room bounds. Exit: player can move around obstacles without clipping.

### Milestone 2 - Melee combat
Add one melee weapon, hit arc, attack timing, enemy damage, hit feedback and dodge. Exit: combat is readable and repeatable.

### Milestone 3 - Firearm + magic
Add one firearm and two skills with cooldowns/energy. Exit: three combat layers have distinct purpose.

### Milestone 4 - Enemy director
Add three enemy archetypes, spawn warnings, threat budget and clear conditions. Exit: room encounter completes deterministically.

### Milestone 5 - Map & minimap
Add 6-room graph, room nodes, route selection, room minimap and transition. Exit: clear a room, choose next node, enter next room.

### Milestone 6 - Reward and run loop
Add three-card upgrade draft, currency, shop/forge room and boss. Exit: complete a full six-room run.

### Milestone 7 - UI polish & audio
Main menu, loadout, pause, results, full HUD, minimap polish, sound, accessibility. Exit: complete run with no placeholder screens.

### Milestone 8 - Save, balance & packaging
Local save/unlocks, performance pass, offline verification and optional Capacitor packaging. Exit: release candidate.

## 14 · QA & ACCEPTANCE
### Core gameplay tests
- **Movement:** Movement is consistent in all directions, collision blocks walls, dodge cannot cross closed boundaries.
- **Melee:** Hit arc matches animation, one enemy is not hit multiple times by one swing unless the weapon explicitly allows it.
- **Firearm:** Ammo, reload, cooldown and projectile collision update correctly.
- **Magic:** Cooldown/energy costs apply once; area effects and statuses expire correctly.
- **Room flow:** One room equals one encounter wave; cleared rooms stop spawning; exit unlocks; room graph never offers an invalid dead end.
- **Minimap:** Player, exit and objective markers stay aligned with world coordinates; discovered enemy markers do not leak hidden information.
- **Rewards:** Three options are distinct; selection applies once; rerolls charge correctly.
- **Save:** Settings and unlocks persist; an interrupted run restores only if checkpoint rules allow it.

### Definition of done - first vertical slice
A player can start a run, enter a 6-room map, clear at least four combat rooms plus one elite and one boss room, choose rewards, use melee/firearm/magic, read the minimap, pause and finish the run. No critical softlocks, no invisible exits, and no UI that blocks combat visibility.

## 15 · ASSET SEARCH CHECKLIST
### Priority order
Find one coherent base pack before collecting individual assets. Start with: (1) top-down arena tileset; (2) one player with 4-direction movement and melee; (3) 3 enemy archetypes; (4) one melee weapon VFX set; (5) one firearm projectile set; (6) 2 magic VFX; (7) HUD/minimap icon pack; (8) audio pack.

### Search terms
- **Environment:** top down pixel art sci fi arena tileset 32x32; top down pixel art dungeon room tileset; modular top down arena tileset
- **Player:** top down pixel character 4 direction melee attack spritesheet; pixel art adventurer slash animation
- **Enemies:** top down pixel art slime enemy spritesheet; pixel art dungeon monster top down 4 direction; top down roguelite enemy pack
- **Combat VFX:** pixel art sword slash effects spritesheet; pixel art projectile impact effects; pixel art magic circle VFX
- **UI:** pixel art game HUD icon pack; minimap icons pixel art; dark roguelite UI icons
- **Audio:** pixel art action game SFX pack; fantasy magic sound effects; dungeon ambient loop

### Asset evaluation
For every asset pack, record source URL, creator, license, attribution requirement, commercial-use permission, editable-source availability, native dimensions, animation frames and whether the art style matches the chosen base pack.
