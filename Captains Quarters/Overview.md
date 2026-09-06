
# Captain's Quarters — Unreal Engine Build Document

### The First-Person Voyage — consolidated design & demo scope

> **Status:** Merge of _The First-Person Voyage_ (engine/corpus-facing draft) and the _Jamie & Rich gameplay session_ (design-facing). This is now the single source of truth for UE5 development. Where the two sources disagreed, the conflict is marked **[CONFLICT]** and left visible rather than silently resolved — those need a decision, not an assumption.
> 
> **Target:** A demo in six weeks. It needs a _taste_ of the mechanics and the storytelling — not the game. **Success metric: players engage for 30+ minutes and come back to it.** Everything in this document is subordinate to that test.
> 
> Markers used: **[OPEN]** needs a decision · **[CONFLICT]** two sources disagree · **[INVENTED]** not in either source, proposed here · **[LOCKED]** decided, build to it.

---

## 1. The pillar

**You are a captain standing on your own deck, and the interface is the ship.**

This is not a new decision. The Visual & Audio Direction already committed to it — _"the world bleeds into the UI, not the other way"_, with the veto: _"Not UI-first. The interface is the ship. If you can tell where the game ends and the menu begins, the design has failed."_ First person is the conclusion of a position already held, not a departure from it.

The register is **weight, not punch.** Naval drama, not arcade. Quiet sells the loud.

Every ambiguity in this document should be resolved by asking: _does this keep the player standing on a deck, or does it put a screen between them and the ship?_

---

## 2. Cold open and first contact **[LOCKED]**

The opening is the most finished thing in the project. Build it as written.

### 2.1 Intro cinematic

**Beat 1 — Darkness.** Water lapping against a dinghy hull. Oars in rowlocks. Fog. Moon obscured. No HUD, no menu, no prompt.

**Beat 2 — The match.** Any input — key, gamepad, mouse — strikes a match. A lantern at the player's feet comes to life; the player holds it out.

**Beat 3 — The rower.** The light finds a figure rowing you along, silent. **[OPEN — see §10.2]** Identity unresolved ("orc or skeleton" is placeholder).

**Beat 4 — The hook.** A gull, distant. A faint light ahead on a shape in the fog. Music: curiosity, muted excitement. The rower speaks — placeholder: _"Rest assured, we will find them. Not today, maybe not tomorrow, but we... will... find them."_ Intent: the player should think _there is something to uncover_. This plants the pursuit thread without exposition.

**Beat 5 — Revelation.** Music bridges. The shape resolves into a port: lanterns by the jetty, moon breaking through. Camera swings to frame the structure, cranes upward, settles on the title — **Captain's Quarters**.

### 2.2 The non-menu

The camera **holds on the title card while the next environment loads behind it.** Ultra Dynamic Sky dials the clock forward to ~08:00–09:00. (This requires UDS to live on the **persistent level**.) Dockside audio fades in — chatter, gulls, crates knocking. Then a coarse voice: _"You there — wake up, man. Have you paid your mooring fees?"_

The camera **reverses its own crane path**, descending to frame the dinghy knocking alongside the jetty. **The rower is gone. The oars are boated.** Only the player character remains, slumped in the stern.

A second shout. The camera closes and **transitions from cinematic camera to pawn camera** — the handover must be seamless. Any input stands the player up, as an animated motion viewed through their own eyes: the player feels the clumsiness of standing.

No menu has appeared. The new game has begun.

**Why this works:** the title card is the loading mask; the night→morning jump reads as elapsed time rather than a cut; and the rower's disappearance is itself a hook.

### 2.3 The diegetic settings problem **[OPEN — see §10.4]**

The harbourmaster takes pity ("you don't look well, let me get you a drink"), leaves you alone in his office, and the room's interactable objects carry what a menu would normally carry. Since the player is already in a new game, no save/load is needed — realistically this is **audio and video settings only**. Player empties their pocket and finds a small ruby in pristine condition, some marlin, a button and a chicken bone. This is a short animated sequence from the player camera and upon this the ruby turns into the players first card! - The first introduction that you are interacting with the world via cards.

No satisfying diegetic metaphor has been found yet. The same principle will eventually be needed for a pause menu. **Risk flagged in source:** diegetic-but-cumbersome is worse than a clean menu. Most players touch settings once.

---

## 3. World structure

### 3.1 Shape **[LOCKED]**

- **Ports are destinations, not a single recurring home base.** Each has different offerings and states. A nice idea Rich and I were floating is to have barkeeps across the land of Romaine keep a lockbox for the player and it can hold a limit of three items. Here you can leave cards behind and take ones that you have stashed VS. thinning.
- **The fog is the run.** Sailing between significant places means crossing it. Entering the fog _is_ entering the procedurally generated encounter sequence.
- This preserves extraction tension (going out is dangerous, arriving is relief) **without** the repetitive home-hub loop.

### 3.2 The map **[LOCKED]**

Captain's Quarters is built on **the existing Romaine world map** — Ironen, Westport, Prista, Rosalia, Telund's Pipe ("the Pipe"), and a maelstrom / "Bermuda Triangle" feature at the centre. New islands or an archipelago may be added to suit CQ.

The world map **starts mostly undiscovered and opens as the player travels.**

**Starting port:** a settlement of wayfarers who all found their way here by one means or another and struggle to leave. They make the best of what they have. This gives the opening location an immediate identity and gives the player a motive — _get out_ — before any larger narrative exists.

### 3.3 Factions **[OPEN — see §10.7]**

No faction system currently exists in Romaine. This is a **worldbuilding opportunity**, not a gap: regions can shift in hostility over time (Westport in upset becomes a dangerous crossing), which feeds the risk heat map in §4.3. Almost certainly **out of scope for the demo**; worth designing so the demo doesn't foreclose it.

---

## 4. Voyage traversal

### 4.1 The hex crossing

Within a fog crossing, traversal is a **hex map**, roughly **3 tall × 5 long** — to be tested by feel, not fixed on paper. The player picks which face to exit through, so routes branch. **Once a direction is chosen, what is behind is locked out.** No backtracking, no free roaming. Forward progress is constant; _which_ encounters you meet is your choice.

### 4.2 The shape of the run**

- An open sea-hex map where _"safe harbour is behind you"_, ports sit at _"varying depth and danger"_, and the central fork is **"push, or turn for home?"** — classic out-and-back extraction, returning to where you started.

### 4.3 Telegraphing **[LOCKED]**

**Agency lives at route selection; mystery lives inside the run.**

- **Inside the fog: shrouded.** You do not see what is on each hex. This is only acceptable _because runs are short_ — a short run with unknowns is exciting; a long one is a slog.
- **At the world-map level: informed.** The player chooses _which crossing to attempt_ using a **regional risk heat map** — some routes pass pirate strongholds, some are calm. High risk, high reward. Information is regional and atmospheric, never itemised ("that area looks dodgy," the way a street reads dodgy on sight), and explicitly **not in-your-face UI**.

### 4.4 Traversal

 Within a {fog} passage, traversal is a **hex map** a rough "3 tall × 5 long" TBD, we will need to test this by feel and play before making it concrete. The player picks which face of the hex to exit through, so routes branch — but **once a direction is chosen, everything behind is locked out.** No backtracking, no free roaming. You're always making forward progress toward the destination, but *which* encounters you meet is your choice

### 4.5 Wind **[OPEN — see §10.5]**

Beside the chart sits the **wind flower** — calm at centre, stronger states on the fringe, harder to reach and harder to hold. Its ring position encodes wind **strength and direction at once**. It is as an abstraction and only says it is _"a small fixed cluster, not the voyage map itself"_; its physical form is TBD, ideas?

Heading is therefore a real decision:

- Run with the wind → the leg is cheap.
- Reach across it → it costs what it costs.
- **Beat into it** → you pay in time and exposure. More sea, more chances for the sea to notice you.

Weather is **local to where you are, not a global clock**, and its job is to **take away your ability to see and plan**, not to block you. The best route is not fixed — it drifts. The map is alive.

Choosing a heading is a quill scratch. The chart is silent but for the sea.

### 4.6 One-use foresight boon

A "magical map" / crystal-ball consumable granting a brief glimpse of what sits on the hexes ahead, then gone — explicitly like flipping tiles in a memory game. Obtainable by trade, purchase, or lucky discovery. Small, characterful, good fit for a reward. The world of Romaine should be filled with such wonderful items for the player to discover.

---

## 5. The passage

Under way, the audio bed is constant: timbers under their own weight, rope against blocks, water at the speed you are making. **You would miss it if it stopped.**

The lookout hails. **Two sightings**, each with a bearing — _to port_, _to starboard_, _abeam_. In first person this stops being vocabulary and becomes literal: **the call comes from above and behind you, and you turn and look.** 

**You close with exactly one.** The others fall astern, you can make one 'abeam' movement' per hex tile, then the remainder of that column gets locked out and you must press forward to port or starboard. That is the cost of the fork.

### 5.1 Loot sightings — the tool hand

Flotsam, a lone sail, a sunk wreck, a derelict, a man in the water. You reach for a **tool** — you hold five from your exploration deck.

- In these types of situations you are using you Force, Focus and Finesse -> Utility Deck.

You keep one thing. **Some things you keep are dual** — Ship's Provisions serves on deck _and_ in the fight, entering both decks. That is the "aha", and it should land as one.

### 5.2 Encounter sightings

No tool hand. There is a person, or a wreck, or a practice a crew keeps at this particular hex that nobody can explain the same way twice. You choose an approach. **How you acquire an officer here sets the loyalty she starts with.**

### 5.3 The passage floor **[LOCKED]**

You cannot be sunk out in the fog, you can be hurt out in the fog; you cannot be ended out there. (Officers, _can_ die — see §7.2.)

--> An idea to keep this dramatic and to make it matter as you cannot lose the ship. If you lose a battle in the fog the 'You Died' equivalent is what is left of your crew in longboats towing your splinter of a vessel back into Rosalia. Here she can be scrapped / sold or you can repair / rebuild her. Of course you would have lost good men, good equipment and cargo upon your return.

We will likely need to discuss this further as it will be validated via playtesting and much tweaking.

---

## 6. The fight

She is on the horizon and then she is not on the horizon.

Wind is read **once, at the start**, as a condition — she sailed into your guns, or she has the weather gauge, or neither. Three seconds, typeset like a log entry, then gone.

You hold **five Orders**. You have **three Command Points**. The Orders fall in three lines, and the lines are honest about what they touch:

|Line|What it touches|
|---|---|
|**Gunnery**|her hull|
|**Seamanship**|your survival — Brace, Resolve|
|**Boarding**|her morale and her crew|

She telegraphs. You read it, decide whether to brace or hold your nerve, and spend.

### 6.1 The Vise **[LOCKED — do not redesign]**

Your strongest Orders cost something **beyond** Command Points. _Press the Gun Crews_ takes two Morale. _Ramming Speed_ takes six Hull — **your** hull.

**You can win every battle and still lose the voyage.**

The cost is **anticipatory, never retrospective** — the hull trembles where it would drop _before_ you commit. The veto is absolute: **never make the cost feel kind.**

### 6.2 Quarter

When she is done, you may be offered **Quarter**. Time slows. The audio bed thins to water and rope. Her flag comes down a foot at a time, by a hand paying out a halyard. A voice calls across the gap, too far to make out.

Grant it or don't — **both are captain's choices**, but the game world remembers your choices and they echo moving forward in one fashion or another. It may be something as simple as one merchant refusing to do business with you on account of ruthless behaviour and yet another path may open as a result, an offer to join a secret guild for example? I am sure you get the idea. Both choice have ramifications and bonuses. The flavour of which begins to shape you as a participant in the world. Your legend begins to take shape.

### 6.3 Officer death

**Morale falls.** A pause. The ship's bell, once, slowly. The crew goes quiet for two beats. Then the world resumes — but not all the way. There is an absence in the audio bed for the rest of the encounter.

---

## 7. The fork and the sea's memory

### 7.1 The fork

You are further out than you were. You have things you did not have. Now the question the whole game is built on: **press on, or turn back?** (Structure pending §4.2.)

**Everything you are carrying is at risk.** Loot, cards, the fleet — all of it goes if the run fails. Your officers' equipment goes with them.

### 7.2 Officers can die **[LOCKED]**

Officers can die out here **regardless of whether the run succeeds**, and this is **explicitly not cushioned**. An officer is a person with a name and a loyalty band; if they die they are gone until you recruit again.

### 7.3 Flotsam — loss as a reason to sail again

What you lose is **not gone forever.** It becomes **flotsam**, and the sea gives things back — **not from a generic table: your gunner's actual cutlass.** You can chase rumours that improve the odds. You can trade with people who dive {islanders?} for what the sea keeps.

**A loss is a reason to go again, not only a punishment.**

And quietly, this is the mystery: **the sea returning things that shouldn't come back _is_ the recovery system.** The folklore turns out to be right, but not in the way anyone thought.

### 7.4 Home?

Is this even worth considering or perhaps there are no homes for old sailors. We all belong to the sea.

---

## 8. The dual deck

### 8.1 What it is — and what already exists

Two decks used in different contexts:

- **Combat deck** — the Order system of §6, for ship-to-ship encounters.
- **Exploration / discovery / utility deck** — for non-combat: going ashore, investigating, digging, opening things, and possibly trading with NPCs.

**Important reconciliation:** this is _not_ a new system to build from zero. We are extending the Watch's **tool hand** (§5.1) from sea-sightings to land and port exploration — islands, towns, sea-caves, people. Treat it as an extension, not an invention. The watch itself is something we likely need to determine how and if it fits well and will stay involved as now the watch happens between hex tiles? 

Reference: **Shroom & Gloom** — a shovel card digs mounds, a torch lights dark spaces, utility cards open chests.

### 8.2 Why it fits

It keeps exploration **card-based rather than first-person-adventure-based**, protecting the game's identity as a deckbuilder. The perspective can be first person, but the player should **not** be running around with WASD equipping a shovel and swinging it. **The deck is still how you interact with the world.**

Crucially, exploration becomes **subject to deckbuilding decisions**: you reach an island with a treasure map and discover you **thinned the shovel out two ports ago**. That is a consequence the player authored — _"they can't be angry at how the game played out."_

### 8.3 The constraint that makes it work **[LOCKED]**

**There must always be more than one way to accomplish a task.** A missing shovel is never a hard wall.

This maps onto the existing **Force / Focus / Finesse** tripod: digging is the _Force_ solution; there must be _Focus_ and _Finesse_ routes to the same outcome, with some cards acting as multi-tools.

**Authoring implication:** every utility card needs siblings. This must be enforced at content-authoring time or the system fails silently in playtest.

Exploration encounters should be **short — five to ten minutes** — but meaningful, and should **reward curiosity**.

---

## 9. Pacing and generation **[LOCKED — a real constraint, not a preference]**

**Not every leg should be combat.** Back-to-back fights turn a crossing into a slog, and the game must never feel like a chore.

- Roughly **one or two ship encounters per crossing.** Not four or five.
- **Non-combat legs as deliberate breathing space** — an uncharted island to take on water, food and timber; or a quiet leg with no encounter at all. This doubles as a mindfulness beat. Players should not feel under constant pressure to **grind**. _There is adventure and wonder in the quiet places of Romaine._
- The feeling on arrival should be **curiosity about the next run, not dread of it.**

**The generation algorithm must carry weights** — by region, by world state, by player condition — so encounter density and hostility are tuned rather than uniformly random. This produces varied, unique crossings across the player base.

**This must be written into the encounter-generation spec directly, not left as guidance.**

---

## 10. Narrative

### 10.1 The honest state

The overarching narrative and end goal **remain undefined**. What exists so far is strong mechanics without a spine. Two positions are both true:

1. If the loop is fun enough, players won't care much about narrative — half the battle is won.
2. But a real story would make it exceptional — a fun game _and_ great storytelling.

### 10.2 The modular / emergent approach

Rather than authoring a fixed narrative, build **modular encounters that link back to one another**, so the overarching story is discoverable via many paths. A character whose story you uncover as you go, rather than a rigid quest ladder.

**Worked example:** you rescue someone adrift during a crossing; their home port happens to be your destination; delivering them earns a **favour owed**, and they know people who can help you.

**Guard-rail — flagged as a real risk:** for a two-man team this can balloon into unmanageable branching dialogue. Keep it on rails deliberately.

### 10.3 Quest chaining

Pattern: arrive at a port → pick up a lead (wanted board, tavern contact) → the lead sets your next destination → cross the fog → arrive with a new thread. **Risk:** this becomes a quest treadmill. The modular approach above is the mitigation.

### 10.4 The tutorial passage **[LOCKED]**

The man who sells you the boat on **Rosalia** needs passage to the next island. That first crossing is the tutorial — light encounters, low danger, he teaches you the ropes, then leaves after the first port.

**It is a tutorial and the player should never feel it is one.** Benchmark: Shroom & Gloom hands you cards and lets you work it out.

### 10.5 The spine — proposal **[INVENTED — for discussion]**

The question _"why is the player going from A to B?"_ is open. The following uses only what already exists and answers it in one move:

**Every crossing is a search.** You were put over the side after a mutiny. The ones who took your ship went into the fog. The starting port is full of people who came in and cannot get out — and that is not a coincidence, it is the maelstrom's nature.

So A→B is not errand-running: **each port holds a fragment of where they went.** You cross because the trail crosses. The rower already said it: _"we will find them."_

The elegance is that **§7.3 becomes the story engine.** The sea gives things back — your gunner's cutlass, yes. And eventually it gives back something that belonged to **them**. Proof they are still out there, delivered by the mechanic you already built. The folklore is right, but not the way anyone thought.

This spine costs almost nothing to author: it needs the mutiny in the cold open (already implied), fragments seeded in ports (already planned as leads), and one flotsam item that isn't yours.

---

## 11. First person — what changes

The Visual & Audio Direction names fifteen soul moments. It was written engine-agnostic, and several assume you can see **your own ship from outside**. On your own deck, you cannot. Roughly nine get stronger; four need re-staging.

### Stronger in first person

- **The Leviathan** — she lights a lantern per attack across black water. A constellation assembling _in front of you_, then gunports opening one by one, muzzles visible.
- **Quarter** — a figure on her quarterdeck across the gap. A voice you cannot quite hear.
- **Man Overboard** — she is in the wake **behind you**. You have to turn to look. The shout repeats fainter each turn until it stops. Nothing pauses for her.
- **Night Action** — the only light is your own lantern and the muzzle flashes. Already proven: it is what the intro does.
- **Weather as third combatant** — rain across your own face, not across a frame.
- **The chart, the hand, the purse, the port interior** — all become real objects and a real room.

### Need re-staging — felt, not seen **[INVENTED]**

- **Listing** — the deck cants under you; the horizon tilts; guns strain in their tackle.
- **Holed** — water through the gratings; the ship heavy and slow to answer.
- **Ablaze** — fire and smoke where you are standing, not on a silhouette.
- **Mutinous** — men visible on **your own deck**, idle, arguing, not at their stations. This may get _better_ in first person.

The Visual & Audio Direction specifies the outside-view version. Someone must decide the felt equivalent — the above is a proposal.

---

## 12. The demo slice — six weeks

### 12.1 What the demo must prove

Players engage **30+ minutes** and **return**. That means it must contain a _taste_ of mechanics **and** storytelling — not a systems sandbox.

### 12.2 **slice scope**

The two sources disagree on demo shape:

- One passage end to end, deliberately excluding multiple ports, the land leg, the fleet, Guardians and the mystery's reveals. Rationale: The heading, the sighting you commit to, the Vise, and the extraction. Any one alone proves nothing; together they are the game. 

### 12.3 **[INVENTED] Proposed merged slice**

Keeping Source A's discipline while honouring the demo's storytelling requirement:

**In:**

- The cold open and non-menu handover (§2) — this **is** the storytelling taste, and it is already the most finished asset in the project.
- **Rosalia** as a walk-in port: jetty, harbourmaster's office, tavern. Small.
- The tutorial passage (§10.4) — the boat-seller's crossing.
- The chart with wind and a local weather state (§4).
- **One** fog crossing with both sighting kinds (§5).
- **One** combat encounter against one enemy (§6).
- The fork (§7).
- Arrival at a second port — 
- Return with cargo, or fail and see the flotsam.

**Out, deliberately:** the full card pool · the third port as a walk-in space · Guardian encounters · the fleet · faction system · the mystery's mid- and late-game reveals · the diegetic settings room (ship a conventional settings screen behind a pause key for the demo; the _opening_ stays clean, which is what matters).

**Scope honesty:** three walk-in ports plus a cinematic intro plus first-person land traversal plus hex navigation plus the Watch plus combat plus dual decks in six weeks is a lot for a two-person team — especially since **first-person interiors are the single most expensive item on the list and the least load-bearing for the 30-minute test.** The recommendation above cuts port count to _one fully realised_ walk-in space, reusing it on return. If the demo must show three ports, recommend two of them be arrival-and-departure only, without interiors.

### 12.4 Engine discipline **[LOCKED]**

**Port the rules, do not re-derive them.** `src/engine/` is the source of truth for combat resolution, the Watch, loyalty, and the meters. That balancing is paid for. Re-deriving it in Blueprints would quietly throw it away.


---

## 13. Open decisions — ranked by how much each blocks the build

1. **The run shape (§4.2).** Out-and-back extraction, or A→B crossing with an abort option? _Blocks: chart UI, navigation code, the fork, and the meaning of "home"._ Recommendation: A→B with run-level abandon.
2. **Combat camera (§6).** Nothing in either source says. The bible's combat section is an explicit placeholder, and the spec's UE5 handoff still speaks in _panel_ nouns — 2D framing carried over unchallenged. _Recommendation: you stand at your own rail; she is a real hull across real water; you may look around but the fight never requires it._
3. **Cards in first person.** The only guidance in the corpus: _"The HTML cards in hand become 3D card actors. Hover/tap is the design contract; the visual treatment is open."_ Hover is a mouse verb with no first-person equivalent. _Recommendation: a physical stack; looking at one brings it up — but this needs a prototype, not a paper decision._
4. **Does the no-on-screen-text rule extend past the intro?** It is written intro-scoped in both sources. But the game demands readable numbers — three orthogonal meters, effective CP cost shown not raw, no hidden maths, telegraphed enemy intent. Those are text. _Recommendation: diegetic-first with an honest exception — brass gauges and a real log for state, plain numbers where legibility beats purity. Decide once, explicitly, so it stops being ambiguous._
5. **Headings: 6 or 8 (§4.4).** Small, but blocks chart and movement.
6. **Where is the player during a passage, and what is the wind flower physically (§4.5)?** _Recommendation: chart table for plotting; wind read off your own sails, flags and sea state when under way, with the flower as an instrument on the table._
7. **Are the tavern, harbourmaster's office and captain's cabin walk-in spaces?** _Recommendation: yes, and small. This is the cheapest thing to get wrong and the most expensive to build twice._ See §12.3 for the demo-scope caveat.
8. **How long is a run?** No target exists anywhere in either source. The only durations come from the **retired** 3-leg structure. Needed to tune hex grid size and pacing. 20-40 mins per passage depending on the route the player takes. They can engage with no more than 8 hex tiles per run. Always moving out of a hex tile either vertically out the top or bottom to move in a lateral format {only once} after which they must move forward either port or starboard out of the front of the hex tile. Then making everything behind them locked out {greyed out}. On a 3x5 hex grid the players can traverse a minimum of 4 tiles or a max of 8, excluding the starting tile.
9. **The rower's identity (§2.1).** "Orc or skeleton" versus the grounded Age-of-Sail register of the Visual & Audio Direction. _This is really a question about how fantastical Romaine is on screen_ — and it governs the entire art direction, not one character. We are leaning on the Skeleton.
10. **The narrative spine (§10.5).** Confirm, adapt, or discard. Discuss further
11. **Diegetic settings (§2.3).** To be discussed.
12. **Faction system (§3.3).** To be discussed.

---

_Studio 8ight — Captain's Quarters — UE5 Build Document. Mark it up._