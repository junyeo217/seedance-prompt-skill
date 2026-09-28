# Keyframes, storyboards, and blockouts

This module handles visual references that organize a generation's start/end state, process states, shot order, composition, blocking, or motion skeleton. It keeps technical input roles separate from semantic meaning. A reference video used here is a generation reference unless the caller explicitly names a different editing master.

Use the narrowest role the caller requested. Do not turn a storyboard into a frame lock, a blockout into a finished scene, or a file marked `LOCKED` into a command to copy every visual property.

## Choose the reference channel

First classify the supplied material:

| Channel | It can provide | It cannot prove by prose alone |
| --- | --- | --- |
| Dedicated first-frame or last-frame input | A technical boundary role when the selected surface exposes and receives that field | That the sentence was bound to the field, that pixels will be identical, or that another surface has the same field |
| Semantic start/end or intermediate image | A visible state, composition, pose, prop state, or camera direction to reach in the story | A hardware-level frame binding or frame-accurate timing |
| Storyboard grid | Reading order, shot sequence, and approximate composition when that scope is requested | Pixel-exact panel reproduction, panel art/style, or automatic technical keyframes |
| Coarse blockout | Paths, blocking, direction, entrances/exits, camera movement, cuts, lighting changes, sound rhythm, or spatial relationships that are explicitly assigned | Final identity, materials, finished scene, or editing-master status |
| Fine blockout | Existing subject/prop/scene structure, actions, layout, camera treatment, and cuts when explicitly assigned | Its gray materials, blank scene, production markers, or a new identity unless separately mapped |

The first/last/intermediate choice is part of the story contract. If a surface's dedicated frame capability is unknown, preserve the caller's requested technical role and reference label in the prompt or working contract, and write `technical binding: unknown` outside the prompt. Do not silently downgrade the request to a semantic reference, and do not invent a field, slot, or API parameter. A semantic alternative may be offered separately when useful, but it does not replace the requested role.

## Dedicated frame binding versus semantic reference

When the caller explicitly requires a technical first-frame role and the selected surface documents that role, keep each input's declaration as its own standalone sentence:

```text
Use @Image1 as the first frame.
This first frame defines the starting composition, subject positions, poses, prop states, scene, and camera direction.

Use @Image2 as the last frame.
This last frame defines the ending composition, subject positions, poses, prop states, scene, and camera direction.
```

These standalone English sentences are a useful interoperability form when the caller and selected surface permit them. They are prompt text, not a universal language or hardware contract. Preserve caller-supplied language and wording when it differs. Confirm the actual dedicated field and attachment on the selected UI/API separately. If the selected surface has no such field, keep the requested technical role visible and report the binding conflict; offer a semantic form separately rather than silently replacing the request:

```text
@Image1 is the semantic start-state reference: begin with its visible subject positions and prop state.
@Image2 is the semantic end-state reference: arrive at its visible subject positions and prop state.
```

Do not weaken an explicitly requested dedicated role into a vague “first-frame reference” when the technical field exists, and do not write the sentence merely to pretend that a field exists. A prose declaration does not establish output aspect ratio, pixel identity, duration, or acceptance. The official source-profile note associates the first frame with aspect-ratio preflight; treat that as surface-dependent guidance and verify the selected surface. Same-ratio first and last images are a sensible compatibility check, not a universal guarantee. When a supported `FIRST_FRAME_I2V` role is actually bound, its supplied first frame carries the full initial visible state; do not require prose to restate every initial attribute. Describe only changes after that state and the scoped roles of other references. If a first frame conflicts with a separate identity, wardrobe, or scene reference, keep those scopes distinct and ask or record the unresolved conflict rather than collapsing an ordinary reference into the first frame.

Assign every input individually. Do not combine first and last roles into one range statement, and do not let a frame image silently supply the identity, wardrobe, or scene unless those attributes are explicitly assigned:

```text
Use @Image1 as the first frame.
This first frame defines the bakery counter, the decorator's starting hand position, and the undecorated cake.
Use @Image2 as the last frame.
This last frame defines the decorated cake and the decorator's hands away from it.
Use @Image3 for the decorator's facial structure, hair, and uniform; the new action and camera follow this shot.
Use @Image4 for the cake's two-tier structure and frosting details; it does not change either boundary composition.
```

The file status `LOCKED` means that the user accepted a current asset as a production reference. It does not add a first-frame field and does not authorize copying its pose, crop, lighting, background, or camera. Use the project reference-role policy for the attributes that may transfer.

## Intermediate keyframes and state order

An intermediate image can anchor a requested process state. It is a semantic state by default. If the caller asks for a dedicated intermediate-keyframe role and the selected surface exposes it, preserve that role; if the capability is unknown, preserve the request and mark its binding unknown instead of silently reclassifying it. Describe the action as reaching the state naturally around the requested moment; do not promise a static hold or pixel-level replication.

When several independent images define ordered states, declare their order first and describe each image separately:

```text
Use @Image1 through @Image4 as keyframes in that order.

Use @Image1 as the first frame.
This first frame defines the empty display case and the clerk's starting position.
@Image2 defines the next visible state: the single package is on the counter.
@Image3 defines the following visible state: the clerk's hand is extended toward the customer.
Use @Image4 as the last frame.
This last frame defines the package only in the customer's hands.

The shot moves continuously through those visible states in order. At the end, the package remains only with the customer.
```

If the caller supplies `0-4 seconds` or asks for a state at `00:04`, preserve the number and label it as an event budget or approximate arrival point. It is not a frame-accurate edit point. If no numerical timing is supplied, use prose phases. A phase list does not force a cut or a fixed number of shots.

## Storyboard grids

A storyboard grid is a sequence and composition guide. State its reading order and the exact scope the caller wants:

- **Order only:** use the panel order and shot count requested; do not transfer panel composition, sketch medium, labels, placeholders, arrows, or panel props unless separately assigned.
- **Order plus approximate composition:** use panel order and approximate shot size/blocking, while replacing board subjects and scene details with their own role-mapped references.
- **Explicit panel timing:** add panel-to-time allocations only when the caller needs event budgets. The times help organize pacing and may raise adherence; they do not guarantee frame-accurate cuts or strict panel reproduction.

The source guidance prefers a compact board, often `≤15 panels`, but that is a recommendation rather than a universal platform ceiling. Do not create a fixed board count or ask for a fixed shot count when the caller has already specified the board.

Use a narrow order-only example like this:

```text
@Image1 is a three-panel storyboard used only for shot order. Read it from left to right, then top to bottom. Do not use its panel composition, line-art medium, text labels, placeholder figures, arrows, or depicted props.
@Image2 defines the only character's facial structure, hair, and clothing.
@Image3 defines the red umbrella's structure and material.

Use the three panels in their stated order as three shots. Shot 1: the character enters the covered walkway. Shot 2: the character opens the red umbrella. Shot 3: the character leaves the frame with the umbrella open. The final visuals use the requested live-action style.
```

When approximate composition is requested, map it explicitly and keep the final subjects separate:

```text
@Image1 provides the shot order and approximate compositions for a four-panel grid. Read it left to right, top to bottom. Do not adopt its monochrome drawing style, labels, or placeholder people.
@Image2 defines Character A. @Image3 defines Character B. @Image4 defines the single table.
Match the approximate framing of each panel while preserving the two-person count, the table's single quantity, and the identities from their mapped references.
```

Do not let the grid's line-art or monochrome medium become the film's look. Do not transfer annotation boxes, captions, borders, arrows, coordinate marks, or placeholder identities as scene content. If a board is supplied only for ordering, its composition is outside scope even when the board visibly contains it.

For a panel timing map, keep the caller's syntax and state the limitation:

```text
Panel 1 is 0-1.5s, Panel 2 is 1.5-2.5s, and Panel 3 is 2.5-4s. Use the panels in that order; do not invent a fourth shot. These intervals allocate event time and do not guarantee frame-accurate edit points.
```

Upload position is a stable numbering aid only. It is not evidence that the first uploaded face belongs to the first story character. Use the caller's explicit mapping, then the story and asset evidence; use upload order as a tie-breaker only when the candidates and slots are genuinely equivalent and an immediate deterministic answer is requested.

## Project blocking-guide boundary

When the project assigns a clean diagram the role `SHOT_BLOCKING_GUIDE`, its policy controls the guide's use. Bind colors or other identifiers in prompt text, keep the camera-facing spatial relationship required by the project, and let the current shot determine camera, framing, crop, style, lighting, and identity. A blocking guide does not replace an `AXIS_REFERENCE` or a character/prop design reference.

Generic marker examples in this module do not override the project policy. The final prompt should prevent production annotations and placeholder graphics from becoming rendered scene content, while preserving any project-required blocking relationship in its declared scope. Do not use a top-down diagram as an unstated substitute for the project's camera-facing blocking guide, and do not put explanatory labels into the guide as if they were final-world objects.

## Coarse versus fine blockouts

Decide the blockout type before writing. Map each geometric subject or prop separately to its final entity; never let an unlabeled geometric figure silently become a new character.

| Type | Keep from the blockout | Replace or exclude |
| --- | --- | --- |
| `coarse` | Motion paths, direction, subject blocking, entrance/exit order, camera position/path/movement, cuts, lighting changes, sound rhythm, and spatial relationships explicitly needed by the brief | Blockout appearance, gray materials, temporary scene, and production aids; add final identities, materials, props, and scene from role-mapped references |
| `fine` | Complete structure, actions, spatial layout, camera treatment, and cuts when requested | Gray or empty treatment, temporary identity, trajectory lines, axes, controllers, camera frustums, and text markers; re-render with the requested final materials and style |

Use a coarse pattern when a motion skeleton is the useful part:

```text
@Video1 is a coarse-blockout reference. Use it only for the motion paths, subject blocking, camera movement, and entrance order described below; do not use its gray geometry, materials, or temporary scene.
The BLUE figure in @Video1 corresponds to Character A. The GREEN geometric object corresponds to the single cart.
@Image1 defines Character A's appearance and clothing. @Image2 defines the cart's structure and material.

Character A pushes the cart along the inherited path and stops beside the doorway. Preserve the assigned blocking and camera movement. At the end, the cart is beside the doorway and Character A's hands remain on its handle.
```

Use a fine pattern when the structure is already complete:

```text
@Video1 is a fine-blockout reference. Preserve the subject structure, action, spatial layout, camera treatment, and cuts. Do not use its gray materials, blank background, or production markers.
@Image1 defines the character's facial structure, hair, and clothing. @Image2 defines the scene's materials and lighting.

Re-render the subject and scene from @Video1 with the mapped identity, materials, and style. Preserve the action and spatial relationships; use the requested ambience and action sound.
```

If the caller asks for a treatment change partway through a blockout, write the boundary and the state that changes. Use numeric boundaries only when the caller supplies or requires them:

```text
Render @Video1 as the final film. From 0-6s, use the blue-hour exterior and cool light. At 6s, as the door opens, transition to the warm interior treatment. Keep Character A's identity and the inherited blocking continuous.
```

Clean or explicitly exclude trajectory lines, coordinate axes, controllers, camera frustums, and text markers before treating a blockout as scene guidance. A partial appendage motion is an uncertainty to record and inspect; it is not a universal ban or a reason to invent a complete action.

## Limit a blockout to its interval

A blockout can govern only part of a clip. State the interval, the dimensions inherited, and the dimensions outside scope:

```text
@Video2 is the action reference for the 20-25 second counterattack only. Use its path and timing only in that interval; do not extend it to the rest of the film and do not bring its gray scene or original texture into the final footage.
```

If the caller has not supplied numeric boundaries, use named stages such as `during the counterattack` and preserve the event scope. Do not expand a partial reference into a whole-film identity, scene, or camera treatment by implication.

## Common checks

Before returning a keyframe, storyboard, or blockout prompt, verify:

- every image has one individually stated role; first and last roles are not compressed into one range;
- a requested dedicated frame role remains visible even when its binding is unknown; the selected surface's actual binding remains a separate verification fact;
- semantic frames and intermediate states are described as visible states to reach, not pixel locks or static holds;
- the first/last aspect-ratio statement is treated as source-profile or surface-specific preflight, not a universal guarantee;
- multiple views of one subject remain one entity and multiple subjects retain their counts;
- a board's reading order, order-only scope, approximate composition scope, and optional timing are not conflated;
- board art, labels, placeholders, arrows, and markers are not silently rendered as world content;
- `SHOT_BLOCKING_GUIDE` and other project reference roles retain their project-specific constraints;
- coarse and fine blockouts are distinguished, each geometric object is mapped, and partial intervals stay partial;
- a blockout video has not been silently promoted to the sole editing master;
- user-supplied times and end states are preserved without a frame-precision claim.

The completed text remains a generation prompt candidate. It does not prove technical slot binding, playback quality, accepted asset status, or output delivery.
