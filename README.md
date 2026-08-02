# Design Your Room with AI Designer (Unofficial IKEA Planner Prototype)

An interactive 3D room planner prototype exploring how a prompt-driven AI layer could remove the biggest friction in room-planning tools when users know what and how they want, but the tool only understands individual products.

> **Disclaimer**
> This is an independent, unofficial prototype created for educational case study, non-commercial, and conceptual purposes only. All product names, designs, and prices shown are illustrative. They are **NOT affiliated with, endorsed by, or representative of Inter IKEA Systems B.V.**, and do not reflect actual IKEA inventory or pricing.
>
> This is a limited prototype. Certain links, buttons, and areas are not fully functional.



## Pain Point

IKEA's current room planner is a capable manual tool, but it assumes the user already knows what to place. In reality, most people start with an intent instead of a shopping list:

- "I want a room that's calm and full of plants."
- "I'm big fan of sci-fi, so I want a galaxy room with an alien bed."
- "I want my room dark and moody because I love reading at night."

Today, translating that intent into products means manually browsing and placing every piece. Users with a clear aesthetic vision but no product knowledge get stuck at a blank room.

## The prototype

This prototype adds an **AI Designer** (BETA) on top of the replica of current IKEA planner experience. The user types a description in plain language, sets a budget, and receives **3 furnished room options**: Essentials, Best Match, and Complete.

- A distinct bed matched to the theme
- Textiles in specific colorways (i.e. duvet, cushions, throw, rug) as purchasable line items
- Wall and floor finishes applied automatically
- Signature accent pieces per theme
- A running total against the stated budget

The engine interprets three things from the description, even when the prompt is too vague: 
- **Theme** (e.g., Scandinavian and Minimal to Sci-Fi, Cyberpunk, Gothic, Pastel, Jungle)
- **Functional Needs** when users specifically state into the description (e.g., work desk, reading corner, extra storage)
- **Budget** to ensure that users are comfortable with their amount of total spending

## How it works

- AI Designer (BETA) interprets your description on-device
- Theme, needs, and budget are parsed by a rules engine over this tagged catalogue
- Design Generation prioritizes a bed-first guaranteed regardless of your budget, then anything you specified (e.g. a desk or a chair), followed by core lighting and storage. Any leftover budget goes to themed decor, and steps down to a cheaper alternative
- Match Your Budget and Complete The Look always reserve enough budget for wallpaper and flooring, while Get The Essentials only keeps them if there is still room after furniture

The interpretation layer in this prototype is a deterministic on-device rules engine using keyword-based theme and needs detection. 

It is deliberately built behind a defined JSON contract ({brief, budget, catalog} → {interp, options}), so the production version swaps this single layer for an LLM call against a live product catalogue without touching the 3D scene, layout logic, or UI. The swap point is exposed as `window.AI_ENDPOINT` in the source.

## How to try it

Try visualizing your room into the description box, or:

*"I need a calm, forest theme room with full of plants and a desk to work from home"*

Then compare how the rooms, colors, and finishes change in each of the 3 options.

## Current scope and known limitations

- Interpretation is keyword-based, not an LLM. Nuanced or contradictory prompts fall back to a disclosed default.
- Save, measurement, checkout, and account features are mockups.
- Layout uses slot-based placement. Items can visually overlap in edge cases and can be repositioned by hand.
- Desktop and mobile are supported, but the experience is designed desktop-first.

## Purpose

Built as a product management and AI product building (vibe coding) case study by identifying a UX gap in an existing product, proposing an AI-application solution beyond a chatbot, and ship a testable artifact that demonstrates the concept end-to-end with the boundary between what the prototype proves in the UX and what the production requires (i.e. a live catalogue and an LLM interpretation layer).
