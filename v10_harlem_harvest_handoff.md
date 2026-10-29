# Harlem Health Rotation — v10 "A Harlem Harvest" handoff

Single-file HTML5 canvas game (`index.html`, ~568 KB, fonts embedded, no network needed).
Repo: `LunaBoog/harlem-health-rotation` (Chris pushes to `main` himself).
Mac folder: `~/Desktop/me/stuff/RPG_games/harlem-health-rotation/`.

Credit line (title screen + About + report): "Inspired by and created using the research and data of Julia DePinto…" (PUBH 698 capstone).
Content rules kept: no calorie/BMI/weight/macro numbers, no comments on how anyone looks, neighbors are composite characters, and HCZ and GreenThumb are named with a non-affiliation note.

## What v10 is
A Stardew-style life sim built around the original four-act research campaign. The research plot is unchanged: Discover, then Analyze (CHS 2020 in R), then the Pitch at the Community Board, then the Pilot. Around it there is now a daily life loop:

- **Clock and calendar:** the day runs 6 a.m. to 2 a.m. (pass out at 2). One game minute is 0.72 s. Fall 1 is a Monday, seasons are 28 days, and the weather can be sun, cloud, rain, wind or snow. Night has a tint with glowing windows and lamps.
- **Home:** an apartment at 147 E 116th St with a bed (sleep gives an end-of-day summary), a TV (weather, Cocina con Abuela on Mon/Thu/Sat teaches recipes, Harlem 411 food-access facts), a stove (cooking), a chest and a fridge.
- **Casita Garden (GreenThumb):** Miss Bernice hands out a hoe and watering can. The garden has six beds, a seed library, a spigot and a compost bin. There are 8 crops: radish, callaloo, recao, ají dulce, collards, kale, sweet potato and calabaza, some of which regrow. Rain waters every bed.
- **Hearts:** 12 neighbors, 5 hearts each. Talking gives +25 per day and gifts use liked/loved/disliked tastes. Birthdays give ×3. Heart events at 2♥ and 4♥ give recipes, seeds, keepsakes and perks.
- **Cooking:** 9 dishes (sofrito, habichuelas, Sunday collards, callaloo pot, sopa de calabaza, mango-chile, escabeche, Health Bucks greens, roast sweet potato).
- **Community Fridge:** you can share produce. Bundles (Greens, Sofrito, Roots, Kitchen, Evidence, Neighbors) work like Stardew's Community Center. Finishing a bundle schedules a **Block Party** with a potluck table.
- **Mail and calendar:** letters arrive over time (welcome, Bernice, Mom, GreenThumb workshop, Market ride, Harvest Day, hearing, party, launch). **Harvest Day** is Fall 20, 9 a.m. to 4 p.m., with a free produce table on 125th St.
- **New research content:** the cards `g_greenthumb` (program), `t_alaimo` (Alaimo 2008, community gardens & produce intake) and `v_bernice` (voice), plus a "grow" principle. They are wired into the pitch options (`st_garden`, `pa_garden`) and the objections.

## Front end
- The title screen is a sunrise skyline with an elevated train, birds and leaves.
- The character creator lets you pick 6 fellows (perks: Dre gets a heart head start, Eli's gifts count +25%, Grace's crops need less water). You can set skin, hair style and color, top, pants, an accessory, your name, the garden name and a favorite dish.
- The HUD has a Stardew-style clock, a 10-slot hotbar (it flips to the top when you stand low on the screen), item toasts, a minimap and a journal card.
- The wooden menu has tabs: Pack I, Quests J, Social F, Cards C, Map M, Recipes R, Notes N, Options O.
- The talk box has a portrait (64×64, five moods), a name plate, hearts and a typewriter effect.
- There is a procedural chiptune score (day, title, garden, evening, night, indoor and party themes) plus ambience (birds, crickets, rain).

## Scoring
`finalScore` now adds hearts ×40, harvested ×4, cooked, shared ×12, bundles ×300 and potluck 250. Grades: S ≥11000, A ≥8500, B ≥6000, C ≥4000. High scores are kept under `hhr9_hiscores`.

## Saves
The save key is `harlem_harvest_v10`. A v9 save (`harlem_food_access_v9`) migrates automatically: research progress, cards, trust and fellow carry over, and the new life starts at home.

## Build (source lives in the Claude workspace, /home/claude/v10)
`python3 build.py` puts `src/[0-9]*.js` in order inside an IIFE, wraps that in `parts/head.html` (with the fonts injected), `parts/tools.css` and `parts/body.html`, and writes `index.html` plus `check.js` (run `node --check check.js`).

Source map:
- 01 core: constants, audio, state, load/migrate
- 02 maps: east, central, garden, home and the interiors
- 03 art: people sprites and portraits
- 03a world: ground, buildings, viaduct, props, seasons, snow, cached layers
- 03b items: crops, items, icons, pack
- 04 content: cards, NPCs, interviews
- 04b lifedata: gifts, birthdays, heart events, recipes, bundles, mail, TV
- 05 world: spots, NPC schedules, peds/cars/critters, movement, interact, farming, objectives
- 05b time: clock, weather, tint, sleep and newDay
- 05c life: hearts, gifts, cooking, fridge, mail, TV, calendar, festivals
- 06 ui: render, HUD, menus, dialog
- 07 analysis
- 08 pitch and battle
- 09 sim and report
- 09b front: title, creator, scoring, fitCanvas
- 09c audio: music
- 10 main: input, loop, dev helpers

Dev helpers: open with `?dev=1`, then use `HHR.pick('dre')`, `HHR.go(map,x,y)`, `HHR.time(h)`, `HHR.day(n)`, `HHR.weather(w)`, `HHR.give(id,n)`, `HHR.hearts(id,n)`, `HHR.act(n)`, `HHR.near(npc)`, `HHR.clear()` and `HHR.blocked(x,y)`.

## Verified (Playwright, headless Chromium)
- Full campaign: 9 interviews, then act 2 analysis (9/9), act 3 pitch and battle, act 4 planner, launch and report. No page errors.
- Life systems: tools from Bernice, till/plant/water by keypress, TV recipe, gifts, a heart event, Greens bundle to party scheduled, calendar, every menu tab.
- Sleep gives a summary and a new day (crop growth, mail, weather). Passing out at 2 a.m. also works.
- Block party with potluck (keepsake). Harvest Day table. Winter (snow, shoveled sidewalks, dusted beds) and spring (blossoms).
- Reachability flood-fill on all 11 maps: every exit, spot and NPC can be reached.
- v9 save migration. Phone portrait 390×844 (canvas pinned to the top, controls below, smaller signs) and landscape. A frame takes about 17 ms.

## Known small things / ideas
- Priya's 2♥ and Brooks's 4♥ both give the 'pen' keepsake (duplicate).
- Crops keep growing in winter. Seasonal crop rules could come later.
- The pitch battle shuffles which cards you're offered, so a thin deck can lose. That's by design: collect more cards and come back.
