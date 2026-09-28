# Performance, Camera, and Audio

Use this reference to translate a story beat into observable performance, physical camera direction, light, transitions, and sound. It is a conditional writing reference. It does not force one visual style, create a video, or replace the caller's project rules.

## Start with what the audience must perceive

The directing order is:

```text
audience-visible change → subject position and observable reaction → necessary camera change → cut or ending → sound
```

When the emotion is only atmospheric, give the model room to choose the specific acting. When the acting needs control, use a small number of cues:

```text
overall emotional direction + triggering event + observable performance + observable camera, light, or sound change
```

Useful cues include a gaze change, a brow or mouth change, one breath, a hand stopping or moving, or a change in body posture. Use only the cues that carry the beat within the caller's permitted performance scope. For expression-only direction, author only the facial-expression change; do not add gaze shifts, head or body movement, gestures, pauses, or other reaction beats from examples or templates. This scoped limit does not impose stillness or fixed gaze on requests without that limit. Do not force a catalogue of microexpressions, and do not turn a hidden cause into an explanatory close-up merely to make a reaction legible. If the audience is meant to remain uncertain, the cause may stay off-screen, unheard, or unnamed while the reaction remains visible.

## No dialogue is not one visual instruction

Distinguish these requests:

| Request | Write | Do not add automatically |
|---|---|---|
| No character dialogue | No dialogue by the named character or within the requested scope. Preserve explicitly requested off-screen narration, other speakers, nonverbal action, and separate SFX or ambience. | Unrequested narration, closed lips, removed signs, or a new silent pose. |
| No vocalization | No voiced sound from the named character or audio layer. Preserve separately requested narration, dialogue by another speaker, SFX, and ambience. | A forced neutral mouth if a yawn or open-mouth action is requested. |
| No lip-sync | Do not synchronize speech. | Removal of an intentional mouth movement that is not speech. |
| No readable text | Do not require the viewer to read a carrier. | Deleting an existing sign or prop unless requested. |

An open mouth can be a silent yawn, breath, cry without voiced sound, or other non-dialogue action. State the intended action and the absence of speech separately. Absence terms apply only to the named character or audio layer: no character dialogue does not remove explicitly requested off-screen narration, and narration is not added unless the caller requests it or assigns that role. Preserve a blank gaze, intentional exterior look, existing signage, and visible objects when they are part of the requested scene. Do not blanket-add “mouth closed,” “no signs,” “no subtitles,” or “neutral expression” to every silent shot.

For dialogue, bind each line to its speaker and preserve the exact supplied wording. State the language and delivery. Add a regional accent only when the user requests it; do not infer one from the writing system. Voice quality, dialogue content, action sound, ambience, and music are separate layers. A voice description does not authorize rewriting the quote, and ambience does not mean music. If speech is requested without supplied words or explicit dialogue-authorship delegation, describe the requested speaking intent without inventing quoted lines; ask only when the missing content would materially change the scene. Explicitly delegated dialogue creation remains permitted within its scope.

```text
<Speaker> says exactly in <language>, with <requested accent only if supplied>, <timbre and delivery>: {exact supplied dialogue}.
<Other characters> listen without adding dialogue; their mouths remain natural for the specified listening action.
Audio separates the spoken voice from <specific action sounds> and <specific room or environmental ambience>.
```

The caller's Voice Sheet owns voice identity across shots. In this project, the caller's No-BGM rule and mandatory video prefix remain in force; this document does not add music, remove an approved sound exception, or replace a Voice Sheet.

## Optional sound and text notation

When sound, dialogue, and displayed text need explicit separation, the official notation is an optional writing aid:

| Content | Markers | Example |
|---|---|---|
| Music | `()` | `(Quiet piano music.)` |
| Sound effect | `<>` | `<The door latch clicks.>` |
| Dialogue | `{}` | `Mina says in Korean: {잠깐만.}` |
| Subtitle | `【】` | `【다음 날】` |

Use only the layers requested and allowed by the caller; the table does not add music, speech, subtitles, or empty sections. Preserve the caller's chosen format and exact supplied words. Do not normalize verbatim text or unrelated parts of a scoped revision into these markers. When `<>` marks sound effects in newly authored text, use ordinary subject names rather than angle-bracketed names so the same markers do not serve two roles; protected caller labels still remain intact. These markers are prompt text, not proof of provider parsing, slot binding, or rendered text.

## Describe a camera as a physical result

A camera term is useful only when it says who or what is being framed and how the visible relationship changes:

```text
camera movement + target subject or landmark + physical starting position + direction/path + arrival composition or state
```

For a room or multi-subject shot, locate the camera in the space, give its height and relationship to the subject, and name the landmarks that should enter, leave, or remain behind the subject. “From the character's point of view” is not enough when the camera side changes the composition. A sufficient camera reference and a clear user instruction take priority over a dictionary lookup.

Use one primary movement for a simple shot. A compound move is allowed when its phases and endpoint matter:

```text
Start at <physical position> on <subject>. Translate laterally toward <landmark>, then rotate gently to keep <subject> readable. End with <arrival framing>; the camera settles only if that finish is requested.
```

Physical position, lens or focus behavior, rig/viewpoint, time manipulation, and compositing are different controls. A pan is a rotation about a pivot; a truck is a lateral camera translation that can reveal parallax. A zoom changes focal length; a dolly changes the camera's physical distance and therefore perspective. Use [`camera-movement-reference.md`](camera-movement-reference.md) when that distinction is the information the request needs.

Static camera is a valid positive direction. Write “the camera remains fixed while the subject continues” or “the frame holds the same composition while room tone continues” when that is the intent. A frame hold after a move, a stable ending, a frozen frame, and a multi-keyframe sequence are separate results:

- **Stable ending:** the camera has arrived and the image or subject can still breathe.
- **Post-move hold:** the camera stops after a described move while live action or sound continues.
- **Frozen frame:** image motion stops at a stated moment; use only when requested.
- **Multi-keyframe sequence:** distinct input states are bound through the actual supported slots; prose labels alone do not guarantee slot binding.

Do not inherit a handheld, shallow-depth, fixed body, fixed ratio, or named stock look from a donor example unless the caller requests or has approved that look in this scope. A named legacy look is conditional. “Same look” preserves the named colour, texture, contrast, or optical quality; it does not silently copy camera movement, duration, dialogue, or sound. Do not apply a global prohibition on static cameras or a global blacklist for any speed word. Choose speed language from the requested visual result and the selected surface.

## Named legacy look preset (opt-in)

The protected GenHQ opening block is preserved here as the named preset `GENHQ_LEGACY_FULL_PRESERVATION`. Use it only when the caller explicitly asks to preserve the full original GenHQ look block and grade template. It is an internal text preset, not a second skill call and not proof that the selected surface supports any field.

```text
Arricam LT, Cooke S4/i primes, 35mm Kodak Vision3 500T, 1.85:1 spherical, T2.8, shallow depth of field, halation on highlights, fine organic grain, lifted milky blacks, low contrast, no sharpening, no HDR.

[GRADE NAME] grade: [hero tone] as the hero tone, [dominant field colour] field, [ground/base tone], [shadow character], [atmospheric quality]. Handheld with micro-drift, never locked off. Naturalistic performance, real dialogue sync, no music.
```

For a request to preserve only the same colour or texture, inherit only the named colour, texture, contrast, or optical attributes; do not import this preset's ratio, camera body, lens, stock, aperture, handheld direction, dialogue-sync instruction, or audio rule. If the preset conflicts with an explicit camera, audio, or caller-approved block, surface the conflict and keep both instructions visible until resolved; do not silently strip either one. The source's global `static` and `fast` restrictions are not adopted here. Static direction and speed words remain request-scoped. Ordinary runtime does not re-call the GenHQ donor.

## Light, blocking, and physical plausibility

State where the light comes from and what it does to the subject, nearby surfaces, and background. If the face is bright, identify a plausible source and direction. Keep the camera's location, subject blocking, light geometry, and spatial axes consistent with the requested shot. An emotional environment is not a substitute for performance: under the project's neutral-state-sheet rule, keep the environment's fixed state neutral and put the emotional change in the actor, sound, or cut.

When an object or person crosses another subject, describe the observable screen relationship and preserve the occlusion order. Use positive spatial anchors such as “the camera is on the table's near-left side,” “the sign stays behind the actor,” or “the second person remains off-camera.” Do not use a mirror flip as a substitute for a physically motivated reverse or new parallax.

## Transitions and closing beats

For a multishot prompt with a requested cut structure, specify the outgoing state and the next entry. Project multishot cut notation uses bracketed time ranges only when the caller has requested or supplied that cut structure; a continuous single take uses prose events rather than invented timestamps. The timestamps describe editorial intent and do not guarantee frame-precise cuts.

For a camera or in-frame transition, use:

```text
outgoing end state → visible trigger or motion → camera/foreground change → incoming arrival state → audio handoff
```

The transition needs an observable arrival state: “the camera moves toward the doorway and ends with the next room fully readable” is more useful than “the camera drifts through.” An endpoint is a writing aid, not a universal duration deadline. Preserve user-supplied timings and let the selected surface own unsupported timing limits.

The external seamless-bridge pattern can inform a generated bridge between two reference videos. It does not make the two videos a multi-master edit, does not splice their pixels, and does not create a dedicated UI mode. The bridge may be generated from their end and start states; classify it by whether the originals are being modified. A short hard cut, match-on-motion, object wipe, light wipe, mask, or morph is chosen by the user's style and story need. No transition family is mandatory.

End a living final beat with a visible state that can continue through the ending: a breath, a small settling movement, a drifting reflection, room tone, or a light change. A calm camera hold is allowed. Do not convert a requested stable ending into “freeze frame,” and do not use a freeze instruction merely because the final composition should be readable.

## Audio design

Name the audible source and its relationship to the image. Keep these layers distinct:

| Layer | Examples of useful instruction |
|---|---|
| Dialogue | Exact words, speaker, language, requested accent, timing, delivery, and breath before the line. |
| Voice quality | Voice Sheet identity, timbre, register, volume, articulation, and emotional restraint. |
| Action SFX | Footsteps, fabric, latch, paper, device vibration, impact, or object contact tied to a visible action. |
| Ambience | Room tone, traffic, wind, rain, appliances, insects, or a distant public space. |
| Music/score | Include only when the caller explicitly permits it; project video clips remain No-BGM. |

For an audio-only change, keep visuals, speech timing, lip-sync, shots, editing rhythm, and unrelated sounds from the master. For a performance prompt, do not use sound to reveal a cause the direction intentionally hides. A reaction to an off-screen sound can remain a reaction to an unidentified source.

After dialogue, leave whatever non-dialogue tail the shot's event requires: breath, movement residue, or ambience. A project rule or caller may reserve a tail for editing, but it is not a universal number or a substitute for listening to the actual take.

## Reusable patterns

### Silent yawn with existing signage

```text
The character yawns silently while looking past the camera; the mouth opens only as part of the yawn, with no spoken words, narration, or voiced speech. Preserve the existing sign in the background and its position; do not replace, remove, or rewrite it. The camera remains fixed at the stated physical position while the yawn completes, the eyes settle into the requested blank gaze, and the room ambience continues. End on a live, stable composition with a small breath still audible.
```

### Reaction with the cause kept hidden

```text
After an unseen off-screen event, the subject pauses, lowers their gaze, and tightens one hand. Show the reaction through those observable changes. Keep the triggering cause outside the frame and unidentified; do not add an explanatory insert, reveal, or new object. The camera makes only the requested measured adjustment, and the room tone continues without a new music cue.
```

### Static camera with a living ending

```text
The camera stays fixed at <physical location and height>; no pan, tilt, translation, or zoom occurs. <Subject> completes <action>. The final composition remains readable while breathing, fabric, light, or room tone continues through the last moment. This is a live hold, not a frozen frame.
```

### Camera-only pan to truck revision

```text
Keep the existing subject, blocking, action, lighting, lens character, duration, and audio unchanged. Replace only the camera move: start on <physical position> and translate laterally to the right past <foreground landmark>, keeping the lens aimed in the same direction so foreground and background show the requested parallax. End on <arrival composition>. Do not rotate the camera around a fixed pivot; this is a truck right, not a pan right.
```

### Conditional bridge

```text
Use @Video1 only for its actual ending state and @Video2 only for its actual opening state. Generate a new bridge: <foreground subject> triggers <one visible action>; the camera or foreground element carries that motion toward <arrival state>; the opening composition of @Video2 becomes fully readable at the end. Transition audio from <before ambience/SFX> to <after ambience/SFX>. Do not edit either original clip or claim a pixel-identical splice.
```

## Status boundary

Prompt validation can establish that the requested layers and boundaries are written. It cannot establish acting quality, camera performance, audio quality, UI support, or an accepted result. Record those as unverified until the actual surface and output are observed.
