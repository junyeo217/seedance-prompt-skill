# Editing and Extension

This reference helps write a Seedance video operation after the requested text operation and the video task have been separated. It is prompt guidance only. It does not execute an edit, inspect a UI, bind an input slot, or claim that a rendered video exists.

## Keep the two decisions separate

Resolve both axes before writing the body:

1. **Requested text operation:** `create`, `check only`, `verbatim`, or a scoped prompt revision.
2. **Video task:** edit an original video, extend it forward or backward, or generate a new video.

An attached video is not automatically an editing master. A video can be a motion, scene, or style reference for generation, and two videos can describe a generated bridge. A pure `verbatim` request preserves the supplied wording even when the wording is not ready for a submission surface; report that status separately rather than silently rewriting it.

## Route the video task

Use the user's explicit operation first, then inspect only the supplied asset facts needed to make the route intelligible.

| Video task | Master and result | Required boundary |
|---|---|---|
| **Video editing** | One original video is the sole editing master. Change only the named visual object, region, or sound. | The original timeline, actions, camera, occlusions, shots, and unrelated audio remain authoritative. |
| **Forward extension** | Create a new segment after the source ends. The source video remains unchanged. | The first frame of the new segment continues from the source video's actual final state. |
| **Backward extension** | Create a new segment before the source begins. The source video remains unchanged. | The final frame of the new segment connects to the source video's actual first state. |
| **Video generation** | Create a new video from text and optional references. | References supply only their declared attributes; no source is promoted to an edit master by attachment alone. |

If the user says only “extend” and the direction is unknown, ask one consolidated direction question. Do not infer forward or backward from the subject's action, filename, or the order in which files were uploaded.

The caller's master tag is authoritative. The examples below use `@Video1` as a placeholder; if the request names `@Video7`, keep `@Video7` throughout the prompt. Do not renumber or replace the caller's tag.

When editing and extending are both requested, preserve the sequence:

```text
edit @Video1 → receive and inspect the actual edited master → extend that actual master
```

Stage two is not ready merely because a stage-one prompt exists. If no edited output has been produced, say that the new master is not yet available and keep the extension as a prepared second step. If the original is untouched and a new subject appears only in the added segment, route the operation as extension and assign the new material to that segment.

## Sole master, references, and scope

The caller-designated master tag, such as `@Video7`, is the sole editing master when the task is an edit. It governs the original scene, subject count, camera position and movement, shot changes, timeline, action trajectories, occlusion relationships, lighting, and audio unless the request explicitly changes one of those items. An optional image, video, or audio reference is a source for a named attribute or motion idea; it is not a second master. State what to take from each reference and what to ignore, including its background, people, framing, or sound when those are irrelevant.

An edit may cover the **whole video** without a time range. A partial edit names the supplied time segment or the observable event that bounds it. Do not invent a detailed timeline from sparse previews. If the whole source cannot be inspected, state the user's requested changes and use this closure:

```text
Except for the objects explicitly modified above, all other visible characters, props, and background elements in @Video1 remain unchanged and are not to be replaced or removed.
```

For a visual edit, name the original subject or region, target subject or attribute, quantity, and affected scope. Preserve every adjacent element that the requested change does not require. For a dynamic replacement, use the original subject's motion slot only when that timing, path, speed, and occlusion can be observed or is explicitly part of the request:

```text
Remove <original subject> from @Video1 and replace it with <target subject> from @Image1 at the same appearance timing, path, speed, and occlusion positions. The original subject does not appear in the final result. All other subjects, props, camera movement, and event order remain as in @Video1.
```

Do not turn a local colour or material edit into a full replacement of the reference scene. “Use the colour from @Image1” assigns colour or grade information; it does not copy @Image1's camera, duration, composition, background, actors, or audio unless those attributes are also requested.

For an audio-only edit, keep visual actions, lip-sync timing, shots, edit rhythm, and all other audio under the sole master. Identify the speaker or sound category, the requested change, the whole-video or partial scope, and the audio that remains:

```text
Edit @Video1 across the whole video, changing only <named dialogue, voice, ambience, action sound, or music>. Keep all visuals, character actions, lip-sync timing, shots, editing rhythm, and every other audio layer from @Video1 unchanged. Use @Audio1 only for <declared target audio role>.
```

When the request removes background music, do not invent replacement audio. Preserve dialogue, lip-sync, ambience, action sound effects, and visuals. When it changes language or voice timbre, preserve the original dialogue content and speaking times unless rewriting them is explicitly requested.

## Ratio and duration conflicts

Read the source video's actual ratio and duration when the information is available and relevant to the selected surface. A mismatch is a surface conflict to report, not permission to silently change an edit into generation. Do not crop, regenerate, split, pad, or re-time the source without the user's direction.

Use a short status note when the selected editing surface locks a source property:

```text
Parameter status: the editing surface may lock the source ratio and approximate duration. The requested change remains an edit; choose whether to keep those source properties or use an explicitly requested generation route before submission.
```

If the source metadata or the target surface cannot be read, do not claim that a conflict has been confirmed. Preserve the explicit intent and mark the unresolved metadata or slot behavior as unverified. An explicit “continue before/after” request remains extension intent even when the extension duration is configured separately. There is no universal tolerance, target length, or platform count in this reference; the selected surface and caller policy own those parameters. User-supplied numeric segments remain intact, and frame-accurate timing is never promised by prose alone.

“Same look” carries only the requested colour, texture, contrast, or optical character. It does not copy the reference's camera, duration, ratio, dialogue, or sound unless the request says so. Project-specific approved look blocks remain in force in their own scope.

## Timeline, action, occlusion, and audio inheritance

The default edit contract is global master inheritance. Add a small number of observable conditions only for a handoff, placement, entrance, exit, or other event whose completion can be identified in the source:

```text
Only after <observable completion of Event A> may <Event B> begin.
Only after <observable completion of Event B> may <Event C> begin.
```

Do not create frame-precise event times from an incomplete sample. An edit can increase the likelihood of temporal alignment, but the prompt does not guarantee pixel or frame identity.

For every visual edit, preserve the source's object count, action order, movement paths, camera relationship, occlusions, and exit state except where the user names a change. For every audio edit, preserve the source's time alignment and unrelated audio. Keep dialogue content and speaking times by default. Separate:

- the words and language of dialogue;
- voice identity, timbre, register, delivery, and requested accent;
- action sound effects;
- room tone and environmental ambience;
- music or score, subject to the caller's policy.

In this project, the caller's mandatory video prefix, No-BGM rule, Voice Sheet, and approved work-specific look exceptions remain authoritative. This reference does not replace or broaden them.

## Forward extension

Write the source's actual final state first. The new segment begins there, then adds the requested event. Keep one continuous instance of each continuing subject; a turn, occlusion, exit, or re-entry does not create a duplicate. Preserve topology, clothing, prop ownership, camera axis, lighting, and the audio environment at the boundary.

```text
@Video1 is the source video to extend forward.

Extend @Video1 forward. The first frame of the new segment continues from the actual final frame of @Video1: preserve <subject posture and orientation>, <prop positions>, <background and spatial relationships>, <camera position and composition>, <lighting>, <audio state>, and <motion trajectory>.

Then, <one requested action or event>. At the end, <observable arrival state>.

Throughout the extension, maintain <identity and clothing>, <key props>, <background layout>, <camera axis>, and <original audio environment>. The continuing subject remains one continuous object without duplication or splitting.
```

Additional references are assigned before the boundary instruction. They may describe identity, clothing, prop design, or sound, but they do not replace the source video's final boundary frame unless the user explicitly requests that change.

## Backward extension

Describe the preceding event first, then state the source video's actual first frame as the end state of the new segment. Keep later-only characters, props, and effects from appearing early.

```text
@Video1 is the source video to extend backward.

Extend @Video1 backward. Before the source video begins, <one preceding action or event>.

The final frame of the new segment connects to the actual first frame of @Video1: preserve <subject posture and orientation>, <prop positions>, <background and spatial relationships>, <camera position and composition>, <lighting>, <audio state>, and <motion trajectory>.

Throughout the extension, maintain <identity and clothing>, <key props>, <background layout>, <camera axis>, and <original audio environment>. The continuing subject remains one continuous object without duplication or splitting. Later-only characters, props, and effects do not appear early.
```

The extension boundary is a continuity goal, not a guarantee of pixel identity. The original segment is not edited at the same time. If the UI offers dedicated first or last inputs, use the actual supported slot only after it is observed; the prose declaration above does not bind an unknown UI slot.

## Bridges between two videos

A seamless bridge can use the ending of `@Video1` and the opening of `@Video2` as references for a **new generated segment**. It is not automatically a two-master edit, a splice of source pixels, or a new execution mode. First decide whether the user wants to change either original. If yes, use the sole-master edit contract. If no, write a generated bridge with explicit reference roles.

Use this bridge order when the request needs it:

```text
outgoing final state → visible trigger action → camera or foreground transition → arrival state → audio handoff
```

Name the start state, one transition action, and the fully readable arrival state. Carry identity, scene logic, subject position, camera direction, motion trend, and audio continuity only to the extent requested. Do not import later events into the outgoing clip. Do not promise a pixel-identical join, a fixed transition deadline, or a particular number of bridge frames unless the caller supplies and the selected surface supports it.

## Output status

Keep these states separate in the handoff:

- prompt drafted or checked;
- source assets and metadata read or unverified;
- operation routed as edit, extension, or generation;
- actual edited master available;
- extension stage ready from that actual master;
- submitted, rendered, played back, accepted, or locked.

Text routing and source treatment do not prove a generated video result. If a ratio, duration, boundary frame, actual first/last slot, or audio input remains unresolved, return the prompt plus a concise choice or status note and do not label it submission-ready.
