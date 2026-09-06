
# Captain's Quarters — Unreal Engine Build Document

### The First-Person Voyage — consolidated design & demo scope

> **Status:** Merge of _The First-Person Voyage_ (engine/corpus-facing draft) and the _Jamie & Rich gameplay session_ (design-facing). This is now the single source of truth for UE5 development. Where the two sources disagreed, the conflict is marked **[CONFLICT]** and left visible rather than silently resolved — those need a decision, not an assumption.
> 
> **Target:** A demo in six weeks. It needs a _taste_ of the mechanics and the storytelling — not the game. **Success metric: players engage for 30+ minutes and come back to it.** Everything in this document is subordinate to that test.
> 
> Markers used: **[OPEN]** needs a decision · **[CONFLICT]** two sources disagree · **[INVENTED]** not in either source, proposed here · **[LOCKED]** decided, build to it.

---

## 1. The pillar

**You are a captain standing on your own deck, and the interface is the ship.**

This is not a new decision. The Visual & Audio Direction already committed to it — _"the world bleeds into the UI, not the other way"_, with the veto: _"Not UI-first. The interface is the ship. If you can tell where the game ends and the menu begins, the design has failed."_ First person is the conclusion of a position already held, not a departure from it.

The register is **weight, not punch.** Naval drama, not arcade. Quiet sells the loud.

Every ambiguity in this document should be resolved by asking: _does this keep the player standing on a deck, or does it put a screen between them and the ship?_

---

## 2. Cold open and first contact **[LOCKED]**

The opening is the most finished thing in the project. Build it as written.

### 2.1 Intro cinematic

**Beat 1 — Darkness.** Water lapping against a dinghy hull. Oars in rowlocks. Fog. Moon obscured. No HUD, no menu, no prompt.

**Beat 2 — The match.** Any input — key, gamepad, mouse — strikes a match. A lantern at the player's feet comes to life; the player holds it out.

**Beat 3 — The rower.** The light finds a figure rowing you along, silent. **[OPEN — see §10.2]** Identity unresolved ("orc or skeleton" is placeholder).

**Beat 4 — The hook.** A gull, distant. A faint light ahead on a shape in the fog. Music: curiosity, muted excitement. The rower speaks — placeholder: _"Rest assured, we will find them. Not today, maybe not tomorrow, but we... will... find them."_ Intent: the player should think _there is something to uncover_. This plants the pursuit thread without exposition.

**Beat 5 — Revelation.** Music bridges. The shape resolves into a port: lanterns by the jetty, moon breaking through. Camera swings to frame the structure, cranes upward, settles on the title — **Captain's Quarters**.

### 2.2 The non-menu

The camera **holds on the title card while the next environment loads behind it.** Ultra Dynamic Sky dials the clock forward to ~08:00–09:00. (This requires UDS to live on the **persistent level**.) Dockside audio fades in — chatter, gulls, crates knocking. Then a coarse voice: _"You there — wake up, man. Have you paid your mooring fees?"_

The camera **reverses its own crane path**, descending to frame the dinghy knocking alongside the jetty. **The rower is gone. The oars are boated.** Only the player character remains, slumped in the stern.

A second shout. The camera closes and **transitions from cinematic camera to pawn camera** — the handover must be seamless. Any input stands the player up, as an animated motion viewed through their own eyes: the player feels the clumsiness of standing.

No menu has appeared. The new game has begun.

**Why this works:** the title card is the loading mask; the night→morning jump reads as elapsed time rather than a cut; and the rower's disappearance is itself a hook.

### 2.3 The diegetic settings problem **[OPEN — see §10.4]**

The harbourmaster takes pity ("you don't look well, let me get you a drink"), leaves you alone in his office, and the room's interactable objects carry what a menu would normally carry. Since the player is already in a new game, no save/load is needed — realistically this is **audio and video settings only**. Player empties their pocket and finds a small ruby in pristine condition, some marlin, a button and a chicken bone. This is a short animated sequence from the player camera and upon this the ruby turns into the players first card! - The first introduction that you are interacting with the world via cards.

No satisfying diegetic metaphor has been found yet. The same principle will eventually be needed for a pause menu. **Risk flagged in source:** diegetic-but-cumbersome is worse than a clean menu. Most players touch settings once.

**For the demo: ship a conventional settings screen behind a pause key.** The *opening* stays clean, which is the part that matters.

### 2.4 The ruby — the first card **[LOCKED]**

*Separated from §2.3 on 2026-09-06: this is not a settings solution, it is the single most important teaching beat in the game and it was buried inside one.*

Alone in the harbourmaster's office, the player empties his pockets: a small ruby in pristine condition, some marlin, a button, a chicken bone. A short animated sequence from the player camera. **The ruby becomes his first card.**

This is the moment the player learns **the world is played through cards** — with no text, no tutorial box, and no menu. It carries the entire premise of the game in one gesture, which is exactly the standard §1 sets.

It also seeds the mystery: a flawless ruby in the pocket of a man put over the side is a question, not a prop.

---

## 3. World structure

### 3.1 Shape **[LOCKED]**

- **Ports are destinations, not a single recurring home base.** Each has different offerings and states. A nice idea Rich and I were floating is to have barkeeps across the land of Romaine keep a lockbox for the player and it can hold a limit of three items. Here you can leave cards behind and take ones that you have stashed VS. thinning.
- **The fog is the run.** Sailing between significant places means crossing it. Entering the fog _is_ entering the procedurally generated encounter sequence.
- This preserves extraction tension (going out is dangerous, arriving is relief) **without** the repetitive home-hub loop.

### 3.2 The map **[LOCKED]**

Captain's Quarters is built on **the existing Romaine world map** — Ironen, Westport, Prista, Rosalia, Telund's Pipe ("the Pipe"), and a maelstrom / "Bermuda Triangle" feature at the centre. New islands or an archipelago may be added to suit CQ.

The world map **starts mostly undiscovered and opens as the player travels.**

**Starting port:** a settlement of wayfarers who all found their way here by one means or another and struggle to leave. They make the best of what they have. This gives the opening location an immediate identity and gives the player a motive — _get out_ — before any larger narrative exists.

### 3.3 Factions **[OPEN — see §10.7]**

No faction system currently exists in Romaine. This is a **worldbuilding opportunity**, not a gap: regions can shift in hostility over time (Westport in upset becomes a dangerous crossing), which feeds the risk heat map in §4.3. Almost certainly **out of scope for the demo**; worth designing so the demo doesn't foreclose it.

---

## 4. Voyage traversal

### 4.1 The hex crossing

Within a fog crossing, traversal is a **hex map**, roughly **3 tall × 5 long** — to be tested by feel, not fixed on paper. The player picks which face to exit through, so routes branch. **Once a direction is chosen, what is behind is locked out.** No backtracking, no free roaming. Forward progress is constant; _which_ encounters you meet is your choice.

### 4.2 The shape of the run **[LOCKED — 2026-09-06]**

**The fog is the run, and a run cannot be abandoned.** Once you enter you are committed: you reach the destination port, or you are towed back to the port you left.

This means **the push-or-turn-back fork does not exist inside a run.** The commitment is made once, at the world map, with the regional heat map (§4.3) in front of you. Everything after that is tactical — which face you exit, which sighting you close with, how hard you press in a fight.

> **Two maps, two rule-sets.** The **world map** of Romaine is free navigation and ports are destinations. The **passage hex map** is the fog: no backtracking, everything aft locks. An earlier draft collapsed these into one and produced a contradiction; they are separate.

**What carries tension through a crossing, now that you cannot leave:** hull damage does not repair until port. Tile 7 is fought in a worse ship than tile 2. That is the ratchet.

### 4.3 Telegraphing **[LOCKED]**

**Agency lives at route selection; mystery lives inside the run.**

- **Inside the fog: shrouded.** You do not see what is on each hex. This is only acceptable _because runs are short_ — a short run with unknowns is exciting; a long one is a slog.
- **At the world-map level: informed.** The player chooses _which crossing to attempt_ using a **regional risk heat map** — some routes pass pirate strongholds, some are calm. High risk, high reward. Information is regional and atmospheric, never itemised ("that area looks dodgy," the way a street reads dodgy on sight), and explicitly **not in-your-face UI**.

### 4.4 Traversal — **six directions [LOCKED]**

**Flat-top hexes in columns.** Six neighbours: **N/S** in your own column (abeam), **NE/SE** into the next column (forward — port and starboard bow), **NW/SW** behind you (aft, greyed). At the top row there is no N; at the bottom no S. "Eight compass directions" was a square-grid artefact inherited from the bible and is wrong for a hex.

> **[TEST] A 3-row grid funnels harder than it reads.** Every forward move shifts you a row, so from the top row your only forward face is SE, and from the bottom row only NE. A genuine two-way fork exists **only from the middle row** — and one move from centre puts you on a boundary. The abeam move is your way back, but it spends that tile's allowance. 5 rows gives real choice throughout. Since supplies drives passage length, **rows and columns must be config from the first line of code, never a hardcoded 3×5.**


 Within a {fog} passage, traversal is a **hex map** a rough "3 tall × 5 long" TBD, we will need to test this by feel and play before making it concrete. The player picks which face of the hex to exit through, so routes branch — but **once a direction is chosen, everything behind is locked out.** No backtracking, no free roaming. You're always making forward progress toward the destination, but *which* encounters you meet is your choice

### 4.5 Wind **[OPEN — see §10.5]**

Beside the chart sits the **wind flower** — calm at centre, stronger states on the fringe, harder to reach and harder to hold. Its ring position encodes wind **strength and direction at once**. It is as an abstraction and only says it is _"a small fixed cluster, not the voyage map itself"_; its physical form is TBD, ideas?

Heading is therefore a real decision:

- Run with the wind → the leg is cheap.
- Reach across it → it costs what it costs.
- **Beat into it** → you pay in time and exposure. More sea, more chances for the sea to notice you.

Weather is **local to where you are, not a global clock**, and its job is to **take away your ability to see and plan**, not to block you. The best route is not fixed — it drifts. The map is alive.

Choosing a heading is a quill scratch. The chart is silent but for the sea.

### 4.6 One-use foresight boon

A "magical map" / crystal-ball consumable granting a brief glimpse of what sits on the hexes ahead, then gone — explicitly like flipping tiles in a memory game. Obtainable by trade, purchase, or lucky discovery. Small, characterful, good fit for a reward. The world of Romaine should be filled with such wonderful items for the player to discover.

---

## 5. The passage

Under way, the audio bed is constant: timbers under their own weight, rope against blocks, water at the speed you are making. **You would miss it if it stopped.**

The lookout hails. **Two sightings**, each with a bearing — _to port_, _to starboard_, _abeam_. In first person this stops being vocabulary and becomes literal: **the call comes from above and behind you, and you turn and look.** 

**You close with exactly one.** The others fall astern. You may make one **abeam** move per hex tile; after that the remainder of that column locks and you must press forward to port or starboard. That is the cost of the fork.

**The Watch IS the movement decision [LOCKED — 2026-09-06].** The hail is not a system sitting on top of navigation — what you choose to look at *is* where the ship goes.

> **Some faces must offer nothing.** If every exit carries a sighting, every tile is an investigation and §9's breathing space disappears. *"Nothing off the starboard bow"* is itself information, and taking the empty face is the quiet route.

> **[OPEN]** The prototype hails **two** sightings; the geometry gives **four** live faces. If the Watch is the movement decision these must be the same number. Four — each either carrying something or empty — is the working assumption. It changes the loot economy per crossing, so settle it before the hail is written.

### 5.1 Loot sightings — the tool hand

Flotsam, a lone sail, a sunk wreck, a derelict, a man in the water. You reach for a **tool** — you hold five from your exploration deck.

- In these types of situations you are using you Force, Focus and Finesse -> Utility Deck.

You keep one thing. **Some things you keep are dual** — Ship's Provisions serves on deck _and_ in the fight, entering both decks. That is the "aha", and it should land as one.

### 5.2 Encounter sightings

No tool hand. There is a person, or a wreck, or a practice a crew keeps at this particular hex that nobody can explain the same way twice. You choose an approach. **How you acquire an officer here sets the loyalty she starts with.**

### 5.3 The passage floor **[LOCKED]**

You cannot be sunk out in the fog, you can be hurt out in the fog; you cannot be ended out there. (Officers, _can_ die — see §7.2.)

--> An idea to keep this dramatic and to make it matter as you cannot lose the ship. If you lose a battle in the fog the 'You Died' equivalent is what is left of your crew in longboats towing your splinter of a vessel back into **the nearest port** (not a fixed home — that would re-create the home base §3.1 removed, and it makes *where* you failed matter). Here she can be scrapped / sold or you can repair / rebuild her. Of course you would have lost good men, good equipment and cargo upon your return.

We will likely need to discuss this further as it will be validated via playtesting and much tweaking.

---

## 6. The fight

She is on the horizon and then she is not on the horizon.

Wind is read **once, at the start**, as a condition — she sailed into your guns, or she has the weather gauge, or neither. Three seconds, typeset like a log entry, then gone.

You hold **five Orders**. You have **three Command Points**. The Orders fall in three lines, and the lines are honest about what they touch:

|Line|What it touches|
|---|---|
|**Gunnery**|her hull|
|**Seamanship**|your survival — Brace, Resolve|
|**Boarding**|her morale and her crew|

She telegraphs. You read it, decide whether to brace or hold your nerve, and spend.

> **The full combat model now lives in `UE5/SPEC_COMBAT.md`** — bearing, the three-deck draw, morale bands and the banked CP meter, with the authoring rules and the guards. This section is the summary; that document is the build contract.

### 6.0 Bearing and the three decks **[LOCKED — 2026-09-06]**

**You never steer. Heading is a state that cards change.** She sits at one of four bearings — bow, port beam, starboard beam, quarter — and each line works differently at each:

| | Bow | Beam | Quarter |
|---|---|---|---|
| **Gunnery** | chase guns — reduced | **broadside — full** | stern chasers — reduced |
| **Seamanship** | full | full | full |
| **Boarding** | **closing to grapple — full** | reduced | none |

**Seamanship is the only line that turns the ship**, and a turning card braces as it turns so it is never a null play. This makes the surprise-opening roll mechanical rather than cosmetic: *she has the weather gauge* now means **she opens on your quarter** and you come about under fire.

**The consequence worth noticing:** a gunnery deck wants the beam; a boarding deck wants the bow. They are not racing for the same position, so bearing is a strategic axis your deckbuilding commits you to.

**Three decks, one hand.** Gunnery / Seamanship / Boarding are separate draw piles and the player **chooses the split** each turn — four Seamanship and one Gunnery when out of position, four Gunnery when alongside. This converts a draw-luck problem into an agency decision.

The rule that keeps it alive: **every line must do something at every bearing** (hence chase guns). A line that is dead weight at a bearing collapses the choice, because you would simply never draw from it. This is the combat twin of the Force/Focus/Finesse rule in §8.3.

**Cheap to adopt:** `src/data/orders.ts` already tags every Order with a `line` — 35 Gunnery, 35 Seamanship, 29 Boarding.

### 6.1 The Vise **[LOCKED — do not redesign]**

Your strongest Orders cost something **beyond** Command Points. _Press the Gun Crews_ takes two Morale. _Ramming Speed_ takes six Hull — **your** hull.

**You can win every battle and still lose the voyage.**

The cost is **anticipatory, never retrospective** — the hull trembles where it would drop _before_ you commit. The veto is absolute: **never make the cost feel kind.**

### 6.2 Quarter

When she is done, you may be offered **Quarter**. Time slows. The audio bed thins to water and rope. Her flag comes down a foot at a time, by a hand paying out a halyard. A voice calls across the gap, too far to make out.

Grant it or don't — **both are captain's choices**, but the game world remembers your choices and they echo moving forward in one fashion or another. It may be something as simple as one merchant refusing to do business with you on account of ruthless behaviour and yet another path may open as a result, an offer to join a secret guild for example? I am sure you get the idea. Both choice have ramifications and bonuses. The flavour of which begins to shape you as a participant in the world. Your legend begins to take shape.

### 6.3 Officer death

**Morale falls.** *(New — player morale currently has no gameplay effect at all in `src/engine/`;
every morale-driven mechanic there is enemy-side. See §6.4.)* A pause. The ship's bell, once, slowly. The crew goes quiet for two beats. Then the world resumes — but not all the way. There is an absence in the audio bed for the rest of the encounter.

---

## 7. Commitment and the sea's memory

### 7.1 The commitment **[revised 2026-09-06]**

There is no mid-run fork. You chose at the world map and the fog closed behind you.

**Everything you are carrying is at risk.** Loot, cards, the fleet — all of it goes if the run fails. Your officers' equipment goes with them.

### 7.2 Officers can die **[LOCKED]**

Officers can die out here **regardless of whether the run succeeds**, and this is **explicitly not cushioned**. An officer is a person with a name and a loyalty band; if they die they are gone until you recruit again.

### 7.3 Flotsam — loss as a reason to sail again

What you lose is **not gone forever.** It becomes **flotsam**, and the sea gives things back — **not from a generic table: your gunner's actual cutlass.** You can chase rumours that improve the odds. You can trade with people who dive {islanders?} for what the sea keeps.

**A loss is a reason to go again, not only a punishment.**

And quietly, this is the mystery: **the sea returning things that shouldn't come back _is_ the recovery system.** The folklore turns out to be right, but not in the way anyone thought.

### 7.4 Home?

Is this even worth considering or perhaps there are no homes for old sailors. We all belong to the sea.

---

## 8. The dual deck

### 8.1 What it is — and what already exists

Two decks used in different contexts:

- **Combat deck** — the Order system of §6, for ship-to-ship encounters.
- **Exploration / discovery / utility deck** — for non-combat: going ashore, investigating, digging, opening things, and possibly trading with NPCs.

**Important reconciliation:** this is _not_ a new system to build from zero. We are extending the Watch's **tool hand** (§5.1) from sea-sightings to land and port exploration — islands, towns, sea-caves, people. Treat it as an extension, not an invention. The watch itself is something we likely need to determine how and if it fits well and will stay involved as now the watch happens between hex tiles? 

Reference: **Shroom & Gloom** — a shovel card digs mounds, a torch lights dark spaces, utility cards open chests.

### 8.2 Why it fits

It keeps exploration **card-based rather than first-person-adventure-based**, protecting the game's identity as a deckbuilder. The perspective can be first person, but the player should **not** be running around with WASD equipping a shovel and swinging it. **The deck is still how you interact with the world.**

Crucially, exploration becomes **subject to deckbuilding decisions**: you reach an island with a treasure map and discover you **thinned the shovel out two ports ago**. That is a consequence the player authored — _"they can't be angry at how the game played out."_

### 8.3 The constraint that makes it work **[LOCKED]**

**There must always be more than one way to accomplish a task.** A missing shovel is never a hard wall.

This maps onto the **Force / Focus / Finesse** tripod (new — it appears nowhere in the prototype, so it is ours to define):

- **Force** — overcome the problem through strength, authority, or aggression.
- **Focus** — understand it through observation, knowledge, and careful planning.
- **Finesse** — solve it through cleverness, deception, precision, or improvisation.

Digging is the _Force_ solution; there must be _Focus_ and _Finesse_ routes to the same outcome, with some cards acting as multi-tools.

**The authoring rule with teeth: every obstacle accepts exactly TWO of the three.** One is a hard wall — the thing §8.3 vetoes. All three makes the tripod decoration, because your deck composition stops mattering. Two of three means you always have a route, but *which* route depends on what you kept and what you thinned. It is lintable: a script can fail the build when an obstacle has fewer than two.

The *flavour* differs by approach, not the outcome — forcing the wreck gets the cargo and wakes something; finessing it takes longer and the fog closes in.

**Implementation note:** the prototype's Watch already matches tools to sightings via `uses` × `respondsTo` with a fit/improvise fallback. Force/Focus/Finesse can simply **be those tags**. This is a naming of something we own, not a new system.

**Authoring implication:** every utility card needs siblings. This must be enforced at content-authoring time or the system fails silently in playtest.

Exploration encounters should be **short — five to ten minutes** — but meaningful, and should **reward curiosity**.

---

## 9. Pacing and generation **[LOCKED — a real constraint, not a preference]**

**Not every leg should be combat.** Back-to-back fights turn a crossing into a slog, and the game must never feel like a chore.

- Roughly **one or two ship encounters per crossing.** Not four or five.
- **Non-combat legs as deliberate breathing space** — an uncharted island to take on water, food and timber; or a quiet leg with no encounter at all. This doubles as a mindfulness beat. Players should not feel under constant pressure to **grind**. _There is adventure and wonder in the quiet places of Romaine._
- The feeling on arrival should be **curiosity about the next run, not dread of it.**

**The generation algorithm must carry weights** — by region, by world state, by player condition — so encounter density and hostility are tuned rather than uniformly random. This produces varied, unique crossings across the player base.

**This must be written into the encounter-generation spec directly, not left as guidance.**

---

## 10. Narrative

### 10.1 The honest state

The overarching narrative and end goal **remain undefined**. What exists so far is strong mechanics without a spine. Two positions are both true:

1. If the loop is fun enough, players won't care much about narrative — half the battle is won.
2. But a real story would make it exceptional — a fun game _and_ great storytelling.

### 10.2 The modular / emergent approach

Rather than authoring a fixed narrative, build **modular encounters that link back to one another**, so the overarching story is discoverable via many paths. A character whose story you uncover as you go, rather than a rigid quest ladder.

**Worked example:** you rescue someone adrift during a crossing; their home port happens to be your destination; delivering them earns a **favour owed**, and they know people who can help you.

**Guard-rail — flagged as a real risk:** for a two-man team this can balloon into unmanageable branching dialogue. Keep it on rails deliberately.

### 10.3 Quest chaining

Pattern: arrive at a port → pick up a lead (wanted board, tavern contact) → the lead sets your next destination → cross the fog → arrive with a new thread. **Risk:** this becomes a quest treadmill. The modular approach above is the mitigation.

### 10.4 The tutorial passage **[LOCKED]**

The man who sells you the boat on **Rosalia** needs passage to the next island. That first crossing is the tutorial — light encounters, low danger, he teaches you the ropes, then leaves after the first port.

**It is a tutorial and the player should never feel it is one.** Benchmark: Shroom & Gloom hands you cards and lets you work it out.

**Keep it SHORT — roughly three tiles, 8–10 minutes [LOCKED — 2026-09-06].** A full 20–40 minute crossing would spend the entire 30-minute evaluation window on the deliberately easiest, lowest-danger content in the game. Passage length is driven by supplies (§4.5), so a short tutorial crossing is a natural consequence rather than a special case.

### 10.5 The spine — proposal **[INVENTED — for discussion]**

The question _"why is the player going from A to B?"_ is open. The following uses only what already exists and answers it in one move:

**Every crossing is a search.** You were put over the side after a mutiny. The ones who took your ship went into the fog. The starting port is full of people who came in and cannot get out — and that is not a coincidence, it is the maelstrom's nature.

So A→B is not errand-running: **each port holds a fragment of where they went.** You cross because the trail crosses. The rower already said it: _"we will find them."_

The elegance is that **§7.3 becomes the story engine.** The sea gives things back — your gunner's cutlass, yes. And eventually it gives back something that belonged to **them**. Proof they are still out there, delivered by the mechanic you already built. The folklore is right, but not the way anyone thought.

This spine costs almost nothing to author: it needs the mutiny in the cold open (already implied), fragments seeded in ports (already planned as leads), and one flotsam item that isn't yours.

---

## 11. First person — what changes

The Visual & Audio Direction names fifteen soul moments. It was written engine-agnostic, and several assume you can see **your own ship from outside**. On your own deck, you cannot. Roughly nine get stronger; four need re-staging.

### Stronger in first person

- **The Leviathan** — she lights a lantern per attack across black water. A constellation assembling _in front of you_, then gunports opening one by one, muzzles visible.
- **Quarter** — a figure on her quarterdeck across the gap. A voice you cannot quite hear.
- **Man Overboard** — she is in the wake **behind you**. You have to turn to look. The shout repeats fainter each turn until it stops. Nothing pauses for her.
- **Night Action** — the only light is your own lantern and the muzzle flashes. Already proven: it is what the intro does.
- **Weather as third combatant** — rain across your own face, not across a frame.
- **The chart, the hand, the purse, the port interior** — all become real objects and a real room.

### Need re-staging — felt, not seen **[INVENTED]**

- **Listing** — the deck cants under you; the horizon tilts; guns strain in their tackle.
- **Holed** — water through the gratings; the ship heavy and slow to answer.
- **Ablaze** — fire and smoke where you are standing, not on a silhouette.
- **Mutinous** — men visible on **your own deck**, idle, arguing, not at their stations. This may get _better_ in first person.

The Visual & Audio Direction specifies the outside-view version. Someone must decide the felt equivalent — the above is a proposal.

---

## 12. The demo slice — six weeks

### 12.1 What the demo must prove

Players engage **30+ minutes** and **return**. That means it must contain a _taste_ of mechanics **and** storytelling — not a systems sandbox.

### 12.2 **slice scope**

The two sources disagree on demo shape:

- One passage end to end, deliberately excluding multiple ports, the land leg, the fleet, Guardians and the mystery's reveals. Rationale: The heading, the sighting you commit to, the Vise, and the extraction. Any one alone proves nothing; together they are the game. 

### 12.3 **[INVENTED] Proposed merged slice**

Keeping Source A's discipline while honouring the demo's storytelling requirement:

**In:**

- The cold open and non-menu handover (§2) — this **is** the storytelling taste, and it is already the most finished asset in the project.
- **Rosalia** as a walk-in port: jetty, harbourmaster's office, tavern. Small.
- The tutorial passage (§10.4) — the boat-seller's crossing.
- The chart with wind and a local weather state (§4).
- **One** fog crossing with both sighting kinds (§5).
- **One** combat encounter against one enemy (§6).
- The fork (§7).
- Arrival at a second port — 
- Return with cargo, or fail and see the flotsam.

**Out, deliberately:** the full card pool · the third port as a walk-in space · Guardian encounters · the fleet · faction system · the mystery's mid- and late-game reveals · the diegetic settings room (ship a conventional settings screen behind a pause key for the demo; the _opening_ stays clean, which is what matters).

**Scope honesty:** three walk-in ports plus a cinematic intro plus first-person land traversal plus hex navigation plus the Watch plus combat plus dual decks in six weeks is a lot for a two-person team — especially since **first-person interiors are the single most expensive item on the list and the least load-bearing for the 30-minute test.** The recommendation above cuts port count to _one fully realised_ walk-in space, reusing it on return. If the demo must show three ports, recommend two of them be arrival-and-departure only, without interiors.

### 12.4 Engine discipline **[LOCKED]**

**Port the rules, do not re-derive them.** `src/engine/` is the source of truth for combat resolution, the Watch, loyalty, and the meters. That balancing is paid for. Re-deriving it in Blueprints would quietly throw it away.


---

## 13. Decision register

### Settled 2026-09-06 — do not re-litigate

| # | Call |
|---|---|
| 1 | **Run shape.** The fog is the run; a run cannot be abandoned. Two maps, two rule-sets. §4.2 |
| 2 | **Combat camera.** First person on your own deck, constrained yaw over port and starboard. |
| 5 | **Headings: six**, not eight. Flat-top hexes in columns. §4.4 |
| 6 | **The Watch is the movement decision.** Some faces offer nothing. §5 |
| 8 | **Run length.** 20–40 min per crossing, 4–8 tiles. Tutorial crossing cut to ~3 tiles / 8–10 min. Grid size is config, driven by supplies. |
| — | **Bearing + three-deck draw + morale bands + banked CP.** `SPEC_COMBAT.md` |
| — | **Supplies moves to the world map**; hull is the in-crossing ratchet; morale is the crew. |
| — | **Failure tows to the nearest port**, never a fixed home. §5.3 |
| — | **Force / Focus / Finesse**, two-of-three authoring rule. §8.3 |
| — | **Reputation stays**, built on existing `setFlag`/`clearFlag`. No faction model. |
| — | **The intro holds on the title**; it does not fade to black. §2.2 |
| — | **Build in UE5, not the prototype.** Guard: every tunable in data/config from line one. |

### Still open — ranked by how much each blocks the build

1. **Where do the three decks physically live, and how is the split set?** The first thing the combat greybox hits. Candidates in §14.
2. **Does the no-on-screen-text rule extend past the intro?** The game needs readable numbers — three meters, effective CP cost shown not raw, telegraphed intent. Written intro-scoped in both sources, never reconciled. *Decide once, explicitly.*
3. **Two sightings or four?** The geometry gives four live faces; the prototype hails two. They must match. §5
4. **Are the tavern, harbourmaster's office and captain's cabin walk-in spaces?** Cheapest thing to get wrong, most expensive to build twice. Demo answer: **one** fully realised interior, reused.
5. **Morale band thresholds and chase-gun ratios.** Numbers, not paper decisions — `[TEST]`.
6. **The rower's identity.** Leaning skeleton. Governs how fantastical Romaine reads on screen — art direction, not one character.
7. **The narrative spine (§10.5).** Confirm, adapt, or discard.
8. **Faction system (§3.3).** Out of scope for the demo; design so the demo does not foreclose it.

---

## 14. What we already own **[added 2026-09-06]**

**We will rarely start from scratch.** Jamie has several hundred — likely thousands — of assets available to modify and refine. Scoping decisions should assume *find and adapt*, not *build*.

Two that change build estimates materially:

- **RDTK — the Roguelike Deckbuilder Toolkit** (in project; reference at `RDTK_TOOLKIT_REFERENCE.md`). Its two pillars are the **Action System** (logic resolves instantly and synchronously; visuals play out as queued Actions) and the **Dispatcher Hub** (pub/sub so statuses, gear and UI react without hard references). Crucially: *"almost everything in RDTK is a Card or a Status"* — health, initiative, poison, artifacts. **Most CQ "systems" are configurations of `Card` + `BP_Status` + a Dispatcher binding, not new machinery.** The Action System is also *exactly* the prototype's pure-reducer-plus-log architecture, which is what kept it debuggable across 100+ batches — so the port preserves the property rather than fighting for it.
- **Ship models** — need work to fit the direction, but they exist.

### 14.1 Where the three decks might live **[OPEN — brainstorm]**

Options, with the trade-off named:

- **Three stacks on the chart table.** You reach into each pile; the act of drawing *is* the allocation — there is no abstract "setting", just five reaches. Maximally diegetic. **Cost:** five interactions per turn unless we add a scoop/multi-take gesture.
- **Three officers offer you their orders.** The Master Gunner, the Sailing Master, the Bosun. *"Four from the Sailing Master."* Ties the draw to the officer fiction, which is a pillar — and makes officers mechanically present every single turn rather than as passive bonuses. **The hook:** losing an officer could impair access to that line. That is the officers-are-people pillar made mechanical, and genuinely frightening. **The risk:** it may be too punishing, and it stacks a second penalty on a loss that already hurts. `[TEST]`
- **Three brass pegs on the binnacle.** A physical setting that *holds its position* between turns. Directly solves the turn-length problem below. Least fictional, most practical.

**The turn-length problem, stated plainly:** every turn now has two decisions — how to split the draw, then what to play. Over a fifteen-turn fight that is fifteen extra interactions, and on many turns the answer is simply "same as last turn". So **the split must persist by default** and be adjusted only when the player wants it changed. Whatever form it takes, it needs to remember.

---

_Studio 8ight — Captain's Quarters — UE5 Build Document. Mark it up._
