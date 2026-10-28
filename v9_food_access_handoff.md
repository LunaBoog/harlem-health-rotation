# v9 Food Access Field Study: Handoff

v9 rebuilds the Harlem Health Rotation around one question: why do low-income Harlem adults miss five-a-day, and what would actually change it? It is still a single `index.html` with no dependencies apart from an optional Google Fonts link, which falls back to system fonts. The save key is `harlem_food_access_v9`, so v8 saves don't collide with it.

## Campaign (four acts, gated)

| Act | Where | Gate to finish |
|---|---|---|
| **D · Discover** | Field Lab, 116 St & Lex, Deli Grocery, Older Adult Center, 125 St, Uptown Fresh Market, Harlem Children’s Zone | 4 interviews, 3 neighborhood data cards, 3 studies, 2 programs, then report to Dr. Brooks |
| **A · Analyze** | R terminal (lab) | 9 interpretation steps on the PUBH 698 CHS 2020 model |
| **P · Pitch** | Studio easel (lab), then the Community Board podium (125 St) | Lock a 5-slot pitch, then finish the 5-question battle at a confidence of 70 or more |
| **I · Integrate** | Map table (lab) | Run a pilot season with at least 1 star, then launch. The impact report follows |

## Harlem Children’s Zone (v9.1)

Julia works at Harlem Children’s Zone on 125th, so HCZ’s real **Healthy Harlem** program is the strongest answer in every act:
- **Discover:** HCZ is its real building at 35 East 125th Street, enterable from 125 St (door at x18); the arrival sign and planner site both show the address. Ms. Andrea, a composite Healthy Harlem staffer, is the open-question interview for the `v_hcz` voice card. The Harvest table gives the `g_hcz` program card (≈50,000 lb of free produce a year, monthly Harvest markets April–November, Health Bucks, Fresh Food Box with Uptown Grand Central; source: hcz.org Healthy Harlem page).
- **Pitch:** `st_hcz` (SNAP-matched evening Harvest markets co-designed with HCZ parents) and `pa_hcz` are the top-scoring options. The best pitch scores 0.88; the best non-HCZ pitch scores 0.84. Both HCZ cards answer the tenants' rep and the budget objections in the battle, and Ms. Andrea can be called as an ally.
- **Integrate:** the HCZ site is an anchor: fit ×1.2 and +0.15 sustainability on every component there.
- A new field note, "Build on trusted institutions," unlocks.
- The footer, Notes tab and report all say HCZ and the city programs are shown for teaching and that the game is not affiliated with or endorsed by them.

## Credit

`CREDIT` reads: “Inspired by and created using the research and data of Julia DePinto, MPH in Public Health Nutrition, CUNY Graduate School of Public Health & Health Policy.” It appears on the title screen, in the page footer, in the Notes tab and at the top of the impact report. Survey cards cite “J. DePinto, PUBH 698 capstone analysis.”

## v9.2: On Location look and feel

This version is restyled to match `on-locations` (On Location · NYC v8) so the series reads as one family.
- **Layout:** the game fills the window. The top bar has pills for the current act (MTA-style bullet), cards, voices, notes, trust and a live score, plus buttons for Quests (J), Cards (C), Map (M), Notes (N), Sound and Reset. The side column is gone.
- **Pop-ups:** Quests, Cards, Map and Notes open as centered pop-ups with tabs between them. Every conversation is a pop-up too, with a portrait header and speech-bubble quotes. The Community Board battle docks its pop-up at the bottom so the scene stays visible.
- **Canvas HUD:** a NEXT UP card (top left, with segmented progress per act), a minimap (bottom right, showing objectives in pink and you in yellow), a contextual hint pill ("SPACE Interview Doña Carmen"), film-style lower thirds with a subway-mosaic accent, and full-screen act title cards with letterbox bars.
- **Start screen:** an animated Harlem night (brownstones with water towers, NYCHA towers, a Metro-North train on the Park Ave viaduct), a marquee logo with bulbs, feature chips, the crew row, START/CONTINUE, HIGH SCORES, Julia's credit, and the line "Part of Moon's educational RPG series."
- **Character select:** a field clipboard with 10 fellows, each with a perk. The perks are Moon (walks 15% faster), Julia (+150 per first-try analysis step), Ana (follow-ups earn 2 trust), Dre (starts with 3 trust), Kai (+75 per first-try study), Nia (+6 board confidence), Sam (+$5K pilot funding), Luz (60-second Survey Sprint), Eli (+75 per keepsake) and Grace (wrong answers are free). Your name goes on the field badge.
- **Scoring:** the live score comes from `finalScore()`. Rows cover cards, first-try interviews, follow-ups, first-try studies, first-try analysis steps, field notes, pitch grade, board confidence, extra hearings (−100), pilot stars, residents reached, trust, keepsakes, Survey Sprint best and wrong answers (−20). Grades are S 7500 / A 6000 / B 4500 / C 3000 / D.
- **Arcade:** launching the pilot leads to a FINAL SCORE screen where rows count up, you enter 3-letter initials, and the HIGH SCORES board updates. High scores live in `localStorage` under `hhr9_hiscores`, outside the save, so Reset never wipes them.
- **Fonts:** fully offline (ui-monospace body, system sans for headings). The Google Fonts link is gone.
- Dev helper `HHR.pick(id,name)` skips character select.

## Systems

- **Data cards (37).** Survey (capstone output), Place (Foodscape / CHP 2018), Study (the capstone's references), Program (Health Bucks, Get the Good Stuff, Green Carts, MarketRide, SNAP-Ed end, La Marqueta), and Voice (composite residents). The evidence wall shows the locked cards with "find it at" hints.
- **Interviews.** Each resident offers an open, a closed and a leading opener. Only the open question yields the card, and the follow-up probe gives +1 trust.
- **Library.** Read an abstract and answer one question to log the study.
- **Analysis lab.** A live R console, a Table 1 composition chart, and a forest plot of the real aORs with hover tooltips. Borough is locked (DUA), and choosing the outcome as a covariate is a trap. Rigor is the count of steps answered right on the first try.
- **Pitch builder.** Options show their backing cards. Missing cards appear dashed and cut that option's score. The pitch is scored on five dimensions (evidence, equity, feasibility, sustainability, voice), with a synergy bonus for two core strategies. Reviewer notes flag weak picks.
- **Pitch battle.** Rendered on the canvas. Five stakeholders each raise one objection, and you answer from a hand of your own cards: strong +18, partial +8, off-topic −8, slogan −6, admitting the gap +4. You can call a neighbor ally once (3 trust, +15). Funding is $60K at a confidence of 90 or more and $50K at 70 or more.
- **Pilot planner.** Six sites and six components, plus hours, language and evaluation knobs. Live KPIs cover reach, priority share, projected servings/day, sustainability, budget and integrated sites, and runs earn 1 to 3 stars. The model is labeled as illustrative. Its effect sizes are anchored to Hollis-Hansen 2019 and Caldwell 2021.
- **Survey Sprint** (Priya, 125 St). A 45-second plaza minigame where you fill four neighborhood-poverty strata. Live CI whiskers shrink at 1/√n. Teaches why the n = 459 reference group widened the CHS intervals.
- **Trust.** Earned from side quests (Pickles, Mr. Chen's glasses, Hector's sign, then the EBT decal for Kwame, a balanced sprint) and interview probes. Spent on battle allies.
- **UI.** MTA-style line bullets for the acts, a station-tablet location toast, side tabs (Quests J, Cards C, Map M, Notes N), gold diamond objective markers, ambient pedestrians, and full-screen sheets for the big tools. Number keys pick choices and ESC closes or cancels.

## Engine changes since v8

- A proper HTML document. v8 was a fragment that relied on host CSS variables.
- Maps are 20×12 strings in `MAPDEF`. Exits are digits, mapped in `EXITS`. Signage lives in `SIGNS`.
- Hotspots (`SPOTS`) cover multi-tile rects, replacing v8's one-tile props.
- Procedural sprites are outlined and cached per facing and frame (`getPersonCanvas`). Portraits are crops of the sprite.
- Dialogs are built as DOM with closure callbacks, with no inline `onclick` strings. ESC runs the `cancel:true` button, or the only button when there is just one.
- The whole state `S` is saved generically. `R` holds runtime-only state.
- `?dev=1` exposes `window.HHR` for teachers and testing: `HHR.act(n)`, `HHR.go(map,x,y)`, `HHR.trust(n)` and the open* tools.

## Content rules kept

There are no calorie, BMI, weight or macro numbers. The BMI findings in Cummins and Caldwell are deliberately omitted. Race/ethnicity results are framed as associations, with the category-aggregation caveat. Voices are labeled as composite characters.

## Verified

The build passes `node --check`. A flood-fill on every map confirms every NPC, hotspot and exit is reachable, with one dead tile behind Marco, which is fine. Headless Playwright playthroughs ran all four acts, the sprint, reload persistence and a 390px mobile layout with no console errors.

## Next ideas

- Real sprites can drop into the `ART` block. Character ids are in `PEOPLE`.
- If the capstone gets a real Harlem partner, make it a site in `SITES` and an option in `PITCH`.
