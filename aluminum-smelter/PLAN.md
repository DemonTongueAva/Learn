# Plan: How an aluminum smelter works (Kitimat, BC)

A single-file interactive explainer (`aluminum-smelter/index.html`) in the same
format as `computational-universe/`: dark scroll-scene layout, Barlow Condensed /
IBM Plex type, canvas and SVG interactives, no build step, works at phone width.

**Anchor case:** Rio Tinto's BC Works in Kitimat (originally Alcan, first metal
1954, rebuilt with prebake AP-family cells by 2015), powered by its own hydro
system at Kemano. Every general idea gets tied back to a concrete Kitimat
detail.

**Reader:** curious, no chemistry background. Goal: by the end they can explain
why a smelter is "electricity turned into metal" and why it was built in a
remote BC fjord.

---

## Narrative arc (scenes)

### 1. Hook: a can is solid electricity
- Open on Kitimat at the head of Douglas Channel: pot rooms over 1 km long, and
  a town planned from scratch around them.
- The central claim: you can't dig aluminum out of the ground. You have to
  pull it apart from oxygen with electricity, and that takes a lot of it
  (~13–15 kWh per kg, about what a household uses in half a day).
- **Interactive:** a counter for "energy in the can in your hand" (≈15 g of
  aluminum → ~0.2 kWh), comparable to running a laptop for a few hours.

### 2. Why here? Water, mountains, and the sea
- The 1950s Kemano project: the Kenney Dam reverses part of the Nechako
  watershed. Water runs west through a tunnel bored through the Coast
  Mountains and drops ~800 m to the Kemano powerhouse, deep inside a mountain.
  An ~80 km transmission line crosses Kildala Pass to Kitimat.
- A deep-water port takes ships of alumina in and sends metal out.
- Honest context: the reservoir flooded Cheslatta Carrier Nation lands (1952),
  and the smelter sits on Haisla Nation territory. One short, factual panel.
- **Interactive:** map plus an elevation profile you scrub along (reservoir →
  tunnel → penstocks → turbines → transmission line → potlines), with a live
  readout of the head and the power available (P = ρ·g·Q·h).

### 3. From rock to white powder (the part that happens elsewhere)
- Bauxite → alumina (Al₂O₃) by the Bayer process at refineries overseas.
  Kitimat receives alumina, not ore.
- Rule of thumb: ~4 t bauxite → ~2 t alumina → 1 t aluminum.
- **Interactive:** a Sankey-style mass-flow strip that also shows the carbon
  (anodes) and electricity feeding the smelter.

### 4. Inside a pot (the core scene)
- Hall–Héroult (1886): alumina dissolved in molten cryolite at ~960 °C. Carbon
  anodes hang down into the bath. Molten aluminum pools on the carbon cathode
  floor. A huge DC current flows top to bottom.
- Net reaction: 2 Al₂O₃ + 3 C → 4 Al + 3 CO₂. The anodes are eaten as the
  oxygen leaves.
- **Interactive:** an animated cross-section of a cell. Hover or tap a layer
  (crust, anode, bath, metal pad, cathode, steel shell, busbars) for a label
  and its temperature. Bubbles rise off the anodes and the metal pad slowly
  thickens. A "feed" button drops an alumina dose and its concentration
  graph spikes, then decays.

### 5. Counting electrons: Faraday's law
- Each Al atom needs 3 electrons, so metal out is set by current.
- **Interactive calculator:** sliders for line current (100–500 kA), current
  efficiency (85–96%) and cell voltage (3.8–4.8 V). Outputs: kg/day per pot,
  kWh/kg, and tonnes/yr for N pots. Preset "Kitimat-class cell" (~400 kA
  range). Show the theoretical minimum energy as a ghost bar so the reader sees
  where the losses go (mostly heat, which the cell needs to stay molten).

### 6. A potline: hundreds of cells in series
- Pots are wired in series, so the same current runs through all of them and
  their voltages add up to over a thousand volts DC. Rectifiers turn the grid's
  AC into DC.
- Side effects: magnetic fields strong enough to shape the metal's flow (cell
  and busbar design is largely magnetic engineering); pot life of several years;
  spent pot lining is a hazardous-waste stream.
- **Interactive:** a zoomable potline diagram where the current "flows" as
  moving dots. Hover a pot to see its voltage. Toggle "magnetic field" to
  overlay field lines and the stirring of the metal pad.

### 7. The supporting cast: carbon, fume, and the cast house
- **Carbon plant:** petroleum coke + pitch → green anodes → baked → rodded.
  An anode lasts ~3–4 weeks. The leftover "butt" is crushed and recycled.
- **Fume treatment:** HF captured by dry scrubbing onto fresh alumina, which
  then goes into the pots, so the fluoride is recycled.
- **Tapping & cast house:** a vacuum crucible sucks metal out of each pot about
  daily. The cast house alloys it and casts ingot, slab or billet for ships.
- **Interactive:** a circular "plant loop" diagram. Click each station to
  expand it, with the material arrows animating between stations.

### 8. Carbon footprint: why the power source dominates
- Direct process emissions (anode CO₂, plus PFCs from anode effects) vs
  emissions from electricity. On hydro, Kitimat sits far below the global
  average set by coal-powered smelters.
- **Interactive:** a stacked bar chart (process vs power) with a toggle for
  the power source: hydro / gas / coal / Kitimat. Also an "anode effect"
  switch showing the voltage spike and PFC burst.

### 9. What's next
- Inert anodes (e.g. the ELYSIS joint venture) give off oxygen instead of CO₂.
- Recycling uses ~5% of the energy of primary smelting. Show where both fit.
- Close back on the can: water falling in the Coast Mountains, now in your hand.

---

## Build notes
- Reuse the design tokens, scene/section scaffolding, progress bar and
  reduced-motion handling from `computational-universe/index.html`. Swap the
  accent to a molten orange/aluminum-grey pairing.
- Canvas for animated scenes (pot cross-section, potline flow), SVG for the
  map/profile, Sankey and charts. No external JS libraries needed.
- Every interactive gets an aria-label, keyboard control, and a static
  fallback caption that states the takeaway.
- Sources section at the end: Rio Tinto BC Works pages, the Kemano/KMP
  public documents, the International Aluminium Institute (energy and emissions
  stats), and a textbook Hall–Héroult reference.

## Facts to verify before writing copy
Current numbers drift, so check these against primary sources:
- Kitimat capacity (~420–430 kt/yr after modernization), pot count and
  technology name (AP40?), and modernization cost/year.
- Kemano installed capacity (~900 MW?), net head, tunnel lengths, T2 tunnel
  completion date, transmission line length.
- Typical cell current, voltage and energy per kg for that cell family.
- Kitimat's CO₂e intensity vs the global average (IAI figures).
- Where Kitimat's alumina currently comes from.

## Milestones
1. Skeleton: all scenes with copy and static SVGs (readable end to end).
2. Core interactives: pot cross-section (4) and Faraday calculator (5).
3. Map/profile (2), potline (6) and plant loop (7).
4. Emissions chart (8), polish, mobile and accessibility pass, sources.
