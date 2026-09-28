# Generation and references

This module compiles a Seedance generation prompt from a brief and the references that are actually available. It is a writing module. It does not upload assets, select a current UI/API limit, generate media, or prove that a downstream surface bound a reference to a technical slot.

Use the smallest set of sections that makes the request unambiguous. The patterns below are reusable structures, not a required payload, JSON schema, or fixed output wrapper.

## Route the request before writing

Keep two decisions separate:

1. **Text operation:** `create`, `check only`, `verbatim`, or `scoped prompt revision`.
2. **Video task:** `generation`, `editing`, `forward extension`, or `backward extension`.

This module owns a new generation prompt. A check-only request receives checks, a verbatim request preserves the supplied text, and a scoped revision changes only the requested area and any directly dependent wording. An editing or extension task goes to its owning reference module even when it also has a generation step.

An attached video is not automatically an editing master. In a generation request, a video reference supplies only the dimensions explicitly assigned to it, such as action, camera movement, pacing, scene, or sound.

## Build the story contract

Before interpreting reference content, extract the facts supplied by the caller. Keep a separate slot for each named person, group, key prop, and scene. The working contract should capture, as applicable:

- subject names and counts;
- relationships, inside/outside and front/back positions, and stable spatial axes;
- actions and their causal order;
- prop ownership, transfers, quantities, and opening/closing or intact/damaged states;
- scene, time, weather, and requested visual treatment;
- exact quoted dialogue, speaker, language, voice role, and on-screen/off-screen status;
- camera, sound, subtitle, and exclusion requirements;
- the requested start state, end state, and any user-supplied timing.

The contract is the factual boundary. Do not merge a named person with another person in a reference, remove a required event because a reference is more visually prominent, or infer a relationship from clothing or posture. A shot number such as `Shot 45` remains a shot number; it is not a 45-degree camera instruction unless the caller says `45 degrees`.

When the brief contains dialogue, keep a dialogue ledger for each requested segment. Preserve the exact words and speaker. A quoted fragment remains a fragment; do not expand it into a new sentence. If the caller delegates dialogue creation, create dialogue only within that delegation. If the brief gives only a speaking intention, show observable delivery and reaction without inventing words.

For a cause-and-reaction beat, reveal the cause before the reaction only when the audience is meant to know the cause. If the brief says to conceal the cause or identity, preserve that information design. Use a reaction, eyeline, sound, or camera shift that supports the intended mystery without forcing the hidden cause into frame.

## Track asset state before assigning roles

Use the actual attachment state as part of the prompt record. Do not treat a filename, upload order, or a written label as an observation. Distinguish prior observation history from present observations, tool capability, and actual inspection permissions; a field name or status label alone establishes none of these. When requested content depends on relevant readable media, establish current observations before using its contents; respect explicit user inspection restrictions and report actual access/tool limits rather than treating historical records as technical blockers.

| Asset state | What can be claimed | Prompt treatment |
| --- | --- | --- |
| Attached and readable | Directly observed appearance, structure, action, camera, or sound features | Inspect it, assign a role, and use only the observed features that fit the story. |
| Attached but damaged or unreadable | The label and the fact that inspection failed | Preserve the label; do not describe its content. Mark the material uncertainty outside the prompt when it affects a decision. |
| Mentioned by the caller but not attached or inaccessible | The caller's label and written role, if any | Preserve the exact label and relationship in the prompt body when it is part of the correspondence. Do not claim an observation or create a replacement reference. Add a short outside status note when the missing state affects a decision. |
| Attached, readable, but unused | The label and the fact that it is not activated | Keep the exact tag/number in a compact `【Unused Assets】` line inside the prompt when the current input requires a complete asset correspondence. Do not assign it a silent role. |
| Local path supplied without a reference label | The path and its supplied order | Create a stable alias separately by media type, record the path under asset understanding, and use the alias consistently. Order is a numbering aid, not identity evidence. |

For a missing reference, keep the caller's exact label and any written role in the prompt body when needed to preserve correspondence, for example `@Image9 is the wardrobe reference.` Add a short outside note such as: `Asset status: @Image9 was mentioned as the wardrobe reference but is not attached; no wardrobe observation was made.` Do not append a long inventory of absent files. If the caller supplied several missing labels, preserve every caller-established label and written role in the prompt body; only the outside status note may summarize their missing state rather than inventing a catalogue.

When the current agent cannot read an attached or named asset, continue from the text that is confirmed. Do not block a draft merely because an observation is unavailable, but mark any unresolved identity, count, ownership, direction, or keyframe decision outside the prompt.

## Map source asset IDs when needed

This reference-mapping guidance also applies when the chosen video task is editing or extension; it does not change that task's owning module or make the request a generation task.

For a new prompt whose JSON or long-text input identifies assets only by opaque IDs, derive the correspondence from the supplied inventory and media types. Preserve existing caller or provider reference tags exactly and reserve all supplied tag numbers before allocating new aliases. Assign unused `@ImageN`, `@VideoN`, and `@AudioN` aliases separately by media type in first-appearance order for untagged IDs; repeated mentions of one ID reuse its alias. This is reference mapping, not a required JSON schema or permission to rename story entities. Replace source-ID references in authorable directions with their tags and keep a compact ID-to-tag association outside the prompt body. Preserve an ID string that the user deliberately supplies as dialogue, on-screen text, or another protected literal.

If the media type or asset correspondence is unknown, ask for the missing information or report the unresolved mapping instead of guessing. Alias assignment does not establish upload order, provider attachment, or technical slot binding; distinguish a proposed mapping from a verified binding outside the body. Apply ID conversion in a scoped revision only when reference mapping is within the requested change. Check-only reviews do not convert the text, and verbatim delivery keeps every original byte and ID.

## Separate source-profile limits from recommendations

The official `sd25-pe 0.1.1` source describes this input profile:

- up to `30` images, each no larger than `4K`;
- up to `10` videos with a combined duration of no more than `30 seconds`;
- up to `10` audio clips with a combined duration of no more than `30 seconds`;
- up to `50` total reference assets across images, videos, and audio.

These are the frozen source-profile figures, not a universal limit for every current UI, API, or downstream product. The source also describes long videos up to `30 seconds`; treat that as source-profile guidance and check the selected surface at submission. Do not claim that a current Higgsfield surface, an API, or another engine has these same values without current evidence.

The source's stability guidance is separate from the hard profile: subject images often work well with `1 to 8` subjects; subject video and audio often work well with `1 to 5` clips or subjects and `5 to 10 seconds` per clip; editing often works well with an original video of no more than `20 seconds` and `1 to 5` reference images. These are recommendations. Exceeding a recommendation does not itself block a prompt when the confirmed hard profile still allows the input.

If the request is evaluated against the frozen source profile and contains `31` images, write an explicit notice such as:

```text
Asset Note: 31 attached images exceed the frozen official 0.1.1 source-profile limit of 30 images. Reduce the set or use a surface with a separately confirmed limit; Prompt wording cannot bypass this input limit.
```

Do not hide the overage by renumbering, silently dropping named assets, or calling the extra files “other assets.” Preserve the exact labels in the asset record and state which assets are selected if the caller asks for a reduction. If the active surface's limit is unknown, say `current surface limit: unknown` rather than converting the frozen profile into a current fact.

## Observe assets without rewriting the story

Inspect readable assets in two passes: first inventory likely roles, then examine in depth only the assets relevant to the story, a conflict, a key event, or an explicitly assigned role. For videos, confirm subjects, principal actions, shot changes, start state, and end state before inheriting any dimension. For audio, confirm sound type, voice quality, language, dialogue content, and intended use when those are relevant.

Keep these information types distinct:

- **Story assignment:** names, ages, relationships, actions, ownership, event order, and ending state stated by the caller.
- **Asset observation:** facial structure, hair, clothing, material, color, layout, action, camera movement, voice quality, or other details directly seen or heard.

Use the following priority when they disagree:

```text
User's explicit specification > prompt description > asset content > filename and metadata > upload order
```

Do not relabel a neutral `person` as a dancer, worker, or performer because of an observed pose. Do not turn a form of address, rank, occupation, or relationship into an unrequested age or personality trait. Use concrete observed features instead of summary labels such as “delicate” or “commanding.”

## Assign roles and preserve cardinality

Every activated asset gets one declared primary role or an equivalent role defined by the caller. The uppercase role names below are this project's vocabulary examples, not mandatory terms for generic callers. A role controls only the attributes named for that role; the current shot controls the rest. Compare each attribute attributed to a reference against the caller's exact permitted subset, not the broader role name or table. For a palette-only reference, fabric, material, and grain are not also authorized transfers; those attributes may still be independently chosen for the current shot within the caller's creative authority.

| Role | Transfer from the reference | Current shot controls |
| --- | --- | --- |
| `CHARACTER_IDENTITY` | Face, age when explicit/confirmed, hair, skin, body proportions, distinctive features | Expression, gaze, pose, hand action, behavior, camera, crop, lighting, background |
| `WARDROBE_DESIGN` | Garment type, silhouette, fabric, color, key details | Pose-dependent folds, visible side, lighting, crop |
| `PROP_DESIGN` | Recognizable form, material, color, identifying details | Position, orientation, scale, contact, open/closed state, lighting |
| `BACKGROUND_GEOMETRY` | Room topology and fixed architectural relationships | Camera, crop, subject placement, time, lighting, color treatment |
| `AXIS_REFERENCE` | Viewpoint surface, eyeline axis, left/right and front/back relationships | Distance, height, lens, crop, action, lighting |
| `SHOT_BLOCKING_GUIDE` | Explicit blocking, direction, positions, and start-to-end path in the guide's scope | Identity, design, camera framing, lighting, style, and the project policy for guide graphics |
| `LIGHTING_REFERENCE` | Light direction, color temperature, contrast, highlight and shadow behavior | Subject, layout, camera, and action |
| `STYLE_REFERENCE` | Texture, contrast, saturation, grain, halation, palette relationship | Story content, identity, pose, camera, and space |

For this project, the project reference-role policy is authoritative for this table. For a generic caller, preserve the caller's role strings and scopes instead of replacing them with this table's vocabulary. A file marked `LOCKED` is an acceptance status, not a command to copy every pixel, pose, camera, crop, light, or background. Do not put `LOCKED image` or `match the locked image exactly` in a model prompt by default. Write the role, the attributes to take, and the attributes the shot will create.

Map required entities one by one, then run an omission audit. Each line in the final role map should identify one subject, group, prop, scene, action, or sound and one primary reference. Do not compress two people into a range mapping.

```text
Character A maps to @Image1; use only facial structure, hair, and clothing shown there.
Character B maps to @Image2; use only facial structure, hair, and clothing shown there.
The single ticket maps to @Image3; use its recognizable paper form and printed mark.
The kiosk geometry maps to @Image4; use its counter and doorway relationships only.
Do not swap the two characters' identities, positions, actions, or dialogue.
```

When a single subject has multiple views, declare that the views jointly define one entity:

```text
Character A is one person. @Image1 supplies the front view of the face and hair; @Image2 supplies the left-side hairline and ear. Use both views for Character A only; do not create a second person.
```

If two named characters have separate suitable references, bind them one-to-one. If one image genuinely contains both people and no independent candidates exist, say that the one image jointly defines the pair and preserve the pair's count. If the mapping of a core identity, prop owner, left/right position, editing master, extension direction, or keyframe role remains indeterminate, ask one consolidated question. A medium-confidence assumption can continue only when it does not change the core result, and the assumption belongs outside the prompt.

Use a video reference selectively. In a generation task, it does not supply character identity, clothing, or the whole scene by default. If its action or camera treatment is already clear and assigned, name only the dimensions to inherit rather than restating every movement. Use an audio reference for its assigned voice or sound role; when written dialogue conflicts with audio content, the caller's written dialogue wins unless reuse of the audio dialogue is explicit.

## Activate only the references needed for each scene

For multiple assets, organize the working map in this order:

```text
role of each asset → subject mapping → grouping by type → subject definitions → scene-by-scene activation
```

Do not activate every available asset merely because it is available. Within the prompt, keep attached but unused references in a compact, identifiable `【Unused Assets】` block:

```text
【Unused Assets】
@Image7 and @Image8 are attached but unused in this generation; they do not supply people, scenes, props, actions, camera, or sound.
@Audio2 is attached but unused; it does not supply dialogue, voice, ambience, action sound, or music.
```

For a long input, use one compact line per media type, but do not omit an exact unused tag or replace it with `other assets`. A reference that is not attached is not an attached-unused asset: preserve its caller-supplied label and role in the prompt body, then add its outside status note when needed.

Use scene-by-scene activation when the same set contains several locations or events:

```text
【Scene 1 | kiosk】
Use Character A from @Image1, Character B from @Image2, the ticket from @Image3, and kiosk geometry from @Image4.
Event: A places the single ticket in B's hand.
At the end: the ticket is only in B's hand; A's hand is empty.

【Scene 2 | outside】
Use Character A from @Image1 and the street geometry from @Image5.
Event: A waits by the doorway.
At the end: B is not added to this scene and the ticket remains with B off-screen.
```

## Choose a generation pattern

Use a short pattern for a simple event. Omit sections that carry no information; do not invent a look, camera move, sound, or reference role to fill a template.

```text
【Generation Goal】
Generate <video type or core event>. The core subject is <subject>; the principal event is <event>.

【Reference Asset Roles】
@Image1 is used for <one subject's specified attributes>.
@Video1 is used only for <action, camera movement, pacing, scene, or sound>.

【Subjects and Relationships】
<Subject and count>. <Stable relationship, ownership, or spatial axis>.

【Event Script】
At the start: <initial visible state>.
Main event: <continuous event or causally linked events>.
At the end: <observable state and ownership>.

【Maintain Consistency】
Keep <only the identities, counts, relationships, props, axes, and other requested continuities> stable.
```

The `At the start`/`Main event`/`At the end` pattern is a state contract, not a demand for a fixed number of shots. One stage may contain causally linked actions when splitting them would damage the event. Conversely, separate stages or shots are useful when the caller requests distinct compositions or cuts. A single continuous shot may be written in prose phases; phases do not become cuts merely because they are listed.

When the project caller's ordinary video contract applies, keep the audio role to diegetic dialogue, ambience, and action sound effects; do not add BGM merely because a generic pattern permits a music role. Preserve an explicitly requested music role only when that caller contract allows it.

## Write stages, shots, and multishot timing conditionally

For a continuous single-shot request, prefer unnumbered stages or prose events unless the caller supplies or requests numeric timing. Preserve user-supplied times exactly. Numeric times describe an event budget or requested beat; they do not promise a frame-accurate edit point or a particular number of generated cuts.

For an explicitly cut multishot sequence, use the project's bracket syntax only when the cut or timing control is requested or required by the caller:

```text
[00:00-00:03] Shot 1: A reaches for the single ticket at the kiosk; the camera observes from the doorway.
[00:03-00:06] Shot 2: B receives the ticket from A; the frame ends with the ticket only in B's hand.
```

The segments must be contiguous and non-overlapping when the caller supplied a complete timing plan. Preserve exact user times rather than silently redistributing them to fit an external target duration. The external total duration, aspect ratio, resolution, and audio setting belong to the selected generation surface. If the surface and the caller's hard timing conflict, report the conflict and wait for the choice; do not silently crop, split, re-time, or reclassify the task. Repeating the requested shot total does not reconcile an additional cut or an unresolved arrival-to-final-cut relationship. If these events cannot be consistently mapped within that total, state the concrete unresolved relationship outside the body or ask one focused question; a reasonable explicit interpretation that preserves the caller's intent is also valid.

For long material, use as many stages as the events require. Give each stage a visible end state and preserve object ownership, count, and causal order. Do not pad a target duration with invented plot events or empty shots. You may allow a handoff, gaze shift, pause, breath, or transition to unfold longer when that preserves the same story.

## Use an optional shot note

The useful GenHQ shot structure is a compact way to decide what a shot needs. It is not a mandatory five-field form. Select the relevant layers:

1. subject and event;
2. camera angle, framing, lens character, or movement;
3. effect, focus, speed, or texture;
4. lighting and atmosphere;
5. transition out and/or in when the sequence contains a cut.

One clear action is a useful compression test when a shot is crowded, not a universal prohibition on linked actions. Keep a single handoff together when its ownership change is the event; write the causal order and end state instead of splitting it for a rule. Likewise, do not impose constant camera motion, a universal “final shot must keep moving” rule, a fixed lens, a fixed camera body, a fixed aspect ratio, a fixed grade, or a global blacklist of ordinary words. The visual treatment follows the brief and the project caller policy.

Put a reference inline where the shot uses it, and do not repeat a sufficient reference's entire action in prose. A final shot may use `Final beat:` when the caller wants explicit sequence closure; it should state the requested ending state and any settling or continued movement that belongs to the story. A deliberate still or held state remains valid when requested.

## Optional multi-image material-to-video pattern

When the caller asks to turn a group of images into one video, treat “one-click video” as a writing pattern, not a new UI mode, button, or automatic generation operation. Specify only what matters, in this order:

```text
[Material Roles]
@Image1 is used for <subject or opening material>.
@Image2 is used for <subject or process material>.
@Image3 is used for <ending material>.
@Video1 is used only for <editing rhythm, transition, subtitle, or sound style>; do not use its identities or scene.

[Arrangement]
Show the images in <the user-specified order, upload order when explicitly chosen, or model-selected thematic order when delegated>.
Keep <named identity, prop, location, and event relationships> consistent.

[Image Motion]
Apply <the requested degree and kind of parallax, push, lateral movement, or local action> to each image.
Keep <appearance, structure, text, or background relationships> stable.

[Visual Treatment]
Use <the requested editing rhythm, transition, graphic, and color treatment>.

[Audio]
Include <the requested dialogue, ambience, action sound, or music role>.
```

If order matters, write the exact sequence. If order is delegated, say so; do not infer semantics from upload order. Bind each named character or product separately. An optional style-reference video contributes only its declared treatment unless the caller assigns more.

## Final generation preflight

Before returning the compiled prompt, check:

- the text operation and video task are correctly separated;
- every required entity has the correct count, role, and one-to-one mapping;
- story assignments are not replaced by asset guesses;
- each used reference has an explicit role and only its named attributes transfer;
- multiple views are declared as one entity when they belong to one entity;
- attached-unused labels remain exact, while unattached labels and their written roles remain in the prompt body with a short, truthful outside status note when needed;
- inaccessible assets have no fabricated observations;
- dialogue, ownership, causal order, end state, and user-supplied times are preserved;
- hidden causes remain hidden when that is the requested audience information;
- hard source-profile figures, recommendations, and current-surface unknowns are labeled separately;
- stages have not been turned into forced cuts and no universal shot count or five-layer form was invented;
- only relevant references and optional layers are present.

The resulting text is a prompt candidate. It is not evidence that the media was generated, that a reference was attached to a dedicated slot, that the output rendered correctly, or that the caller accepted the asset.
