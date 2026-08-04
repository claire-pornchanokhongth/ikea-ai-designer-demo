# Design Your Room with AI Designer (Unofficial IKEA 3D Room Planner Prototype)

An interactive 3D room planner prototype exploring how a prompt-driven AI layer could remove the biggest friction in room-planning tools when users know what and how they want, but the tool only understands individual products, and usually consumes more than an hour of planning.

> **Disclaimer:**
> This is an independent, unofficial prototype created for educational case study, non-commercial, and conceptual purposes only. All product names, designs, and prices shown are illustrative. They are **NOT affiliated with, endorsed by, or representative of Inter IKEA Systems B.V., and do not reflect actual IKEA inventory or pricing.**
>
> This is a limited prototype. Certain links, buttons, and areas are not fully functional.



## Focused Pain Point

IKEA's current room planner is a capable manual tool, but it assumes the user already knows what to place. In reality, most people start with an intent instead of a solid shopping list:

- "I want my room dark and moody because I love reading at night."
- "I'm a big fan of sci-fi, so I want a galaxy room with an alien bed."
- "I want a room that's calm and full of nature."

Today, translating that intent into products means manually browsing and placing every piece. Users with a clear intent and aesthetic vision but no product knowledge often get stuck at a blank starting room.

## The Prototype

This prototype adds an **AI Designer (BETA)** on top of the replica of current IKEA planner experience. The user types a description in plain language, sets a budget, and receives **3 starting furnished room options** instead of a blank one to start with in just **under 1 minute**: 

- *Get The Essentials*: The comfortable bedroom including what you need 
- *Match Your Budget*: The most reflective from your description balancing with the budget
- *Complete The Look*: The full look of your theme with comfort and decor extras from very few additional budget

With each working under the logics:
- A distinct bed matched to the theme
- Textiles in specific colorways (i.e. duvet, cushions, throw, rug) as purchasable line items
- Wall and floor finishes applied automatically
- Signature accent pieces per theme
- A running total against the stated budget

The engine interprets three things from the description, even when the prompt is too vague: 
- **Theme** (e.g., Minimal, Loft, Monotone, Pastel, Sci-Fi, Cyberpunk, Gothic, Jungle)
- **Functional Needs** when users specifically state into the description (e.g., work desk, reading corner, extra storage)
- **Budget** to ensure that users are comfortable with their amount of total spending

## How it works

- AI Designer (BETA) interprets user description
- Theme, needs, and budget are parsed
- Design Generation prioritizes a bed-first guaranteed regardless of user's budget, then anything the user specified (e.g. a desk or a chair), followed by core lighting and storage. Any leftover budget goes to themed decor, and steps down to a cheaper alternative
- Match Your Budget and Complete The Look always reserve enough budget for wallpaper and flooring for user aesthetic, while Get The Essentials only keeps them if there is still room after furniture

The interpretation layer in this prototype is a deterministic on-device rules engine using keyword-based theme and needs detection. 

It is deliberately built behind a defined JSON contract ({brief, budget, catalog} → {interp, options}), so the production version swaps this single layer for an LLM call against a live product catalogue without touching the 3D scene, layout logic, or UI. The swap point is exposed as `window.AI_ENDPOINT` in the source.

## The Pricing Logics behind each choice

- **Get The Essentials**: Because the core intent of any users choosing this option is to save most out of their budget, this option aims to spend only *30-50%* of the user's maximum budget.
- **Match Your Budget**: This option allows user to optimize the budget fully for the best possible quality and match. The target spend is aimed at *85-100%* of user's target budget.
- **Complete The Look**: Users choosing this path prioritize prompt accuracy and demonstrate budget flexibility. Recommending products at *100-110%* of their target budget ensures they achieve their ideal room aesthetic, while strategically increasing IKEA's sales. 

## Try it yourself

1. Try visualizing your room into the description box, or:

> *"I need a calm, forest theme room with full of plants and a desk to work from home"*

You could type in your prompt perfectly or vaguely, or select from pre-prompted choices available

2. Set your budget

3. Compare how the rooms, colors, and finishes change in each of the 3 options

4. Select what matches your thought the most, then finalize your room!

> This is where you could either seeking further AI assistance or manually add items to your room

## Current Scope and Known Limitations

- This prototype only picks up bedroom planner to test the core idea before scaling through every IKEA Room Planner as intended rapidly.
- Save, measurement, checkout, and account features are mockups.
- Limited mock products (484 items) lead to some generated results that might not fully match user prompt.
- Interpretation is keyword-based, not an LLM. Nuanced or contradictory prompts sometimes fall back to a disclosed default.
- Using Internal CSS for a single-page prototype to test the idea swiftly.
- Layout uses slot-based placement. Items can visually overlap in edge cases and can be repositioned by hand.
- Desktop and mobile are supported, but the experience is designed desktop-first.

## Purposes

This is built as an AI product building (vibe coding) and management case study to identify a UX gap in an existing product, proposing an AI-Enabled solution beyond a chatbot, and ship a testable artifact that demonstrates the concept end-to-end with the boundary between what the prototype proves in the UX and what the production requires (i.e. a live catalogue and an LLM interpretation layer).
