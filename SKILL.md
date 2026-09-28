---
name: seedance
description: Use when a user asks to create, check, preserve, or narrowly revise a Seedance 2.5 video prompt for single-shot or multishot work, including omni reference, with optional text, image, video, audio, keyframe, storyboard, blockout, editing, or extension references. Returns text only and never generates, submits, installs, or updates.
metadata:
  skill_version: "0.1.1+local.5"
  owner: seedance
  tags:
    - seedance
    - prompt-optimization
    - multimodal-video
  upstream:
    package: sd25-pe
    version: "0.1.1"
    source: ".omo/drafts/sd25-pe-0.1.1-SKILL.md"
    source_sha256: "ec77264f589b0ac0b5620964f47cc046c292d9a14706c234067645dfd3547601"
    zip_sha256: "c9c765aa5ba9fa84e8a27ee606f7b8c6229bfb775138133f366ea1ad37b97cba"
    source_role: "Provenance only; this path is not a runtime file dependency."
    derivation: "Local routing and preservation adaptation; the frozen upstream source remains separate."
  required_capabilities:
    filesystem_read: true
    filesystem_write: false
    tool_use: true
    network: false
    binary_outputs: false
  io_contract:
    output_kind: text
    primary_outputs:
      - optimized_prompt
      - review
      - verbatim_prompt
    delivery_notes: outside_prompt
  provenance: "Derived from official sd25-pe 0.1.1; local version 0.1.1+local.5."
---

# Seedance 2.5 prompt entrypoint

## Purpose and boundary

This candidate is the local text-authoring entrypoint for Seedance 2.5. It turns a user's brief or existing prompt into one complete prompt, a review, or an exact verbatim payload. It can read available text or media references when the current environment exposes them, but it never claims to have inspected an inaccessible asset.

Prompt writing is separate from execution. This skill does not generate media, upload or submit assets, call a model, use a network, install or update a skill, open a provider UI, or write files. A prompt, review, or submission-ready text is not proof of an upload, UI binding, render, playback, acceptance, or delivery.

Use plain text decisions; do not require a new JSON payload or schema. The caller's language controls the surrounding output. User dialogue, source-language text, reference tags, and authored time notation remain protected.

## Guards before template selection

Make two separate decisions before choosing a generation, editing, extension, or other writing template.

1. **Choose the text operation.**

   - **create**: author a new complete prompt from the request.
   - **check only**: inspect the supplied prompt and return a review. Do not rewrite it or return a submission-ready replacement.
   - **verbatim**: return the designated prompt byte-for-byte, including language, whitespace, line breaks, quotes, tags, and ordering. Do not template, normalize, translate, or add blocks. If a mandatory project block is missing, report that outside the verbatim payload.
   - **scoped prompt revision**: change only the portions the user requested and the smallest necessary linkage; return the complete revised prompt, not a diff.

   If the requested text operation is genuinely ambiguous, ask one focused question before writing. Do not let a request to check become a rewrite or let a verbatim request become a cleanup.

2. **Choose the video task independently.**

   - **generation**: make a new video from text and optional references. Multi-reference work, keyframes, storyboard grids, and blockouts are modules of generation.
   - **editing original**: use one sole original video as the editing master and change the named object, region, or sound while preserving the rest. A full-video edit does not require a time range.
   - **extension**: add new material before or after an existing video. Keep the direction and boundary state explicit; do not rewrite the original segment. If editing and extension are both required, edit first and use the resulting master for the extension.

   Do not infer editing from words such as convert, adjust, change, or keep unchanged. Use the user's explicit operation and any confirmed surface facts. Do not impose universal counts, durations, ratios, frame rates, or sound settings; preserve user-authored numbers and defer surface parameters to the actual caller or provider.

The first decision controls how text may change. The second controls which video reference module is needed. Neither decision is silently replaced by the other.

## Protected content

Before create or scoped revision, establish the smallest internal story and text contract needed for the request. Preserve:

- every named subject and its count;
- story facts, causal order, scene, spatial relationships, and ending state;
- key objects, ownership, transfers, and physical state;
- explicit timing, including bracketed multishot cut notation when the caller uses it;
- quoted dialogue, quoted fragments, speaker, language, on-screen or off-screen role, and assigned audio;
  - user-established prompt reference labels and roles, without renumbering or dropping them from the prompt body; outside status notes are additional;
- caller-approved exclusions, look blocks, and project-specific policies.

Do not turn an asset observation into a story fact. A metadata label such as LOCKED is a production status, not an instruction to copy every pose, expression, camera, crop, light, or background property. Do not reveal a hidden cause merely to make a reaction easier to describe. If a quoted fragment is the only dialogue supplied, keep only that fragment as spoken words. A request for a conversation or speaking behavior alone is not explicit delegation to invent quoted lines. Dialogue explicitly delegated to the author may be created within the delegated scope.

For a scoped camera-only revision, preserve dialogue, timing, speaker and audio roles, reference tags, story facts, and all non-camera instructions. Change a linked event sentence only when that linkage is necessary to make the requested camera change coherent.

## Selective reference loading

Read only the references needed for the chosen operation. These links are the integrated candidate's peer modules. If a required peer is missing at use time, report the missing resource and do not invent its content.

| Need | Read |
|---|---|
| New generation, multi-reference or source-ID mapping, scene/action structure | [generation and references](references/generation-and-references.md) |
| Original-video editing, audio editing, forward or backward extension | [editing and extension](references/editing-and-extension.md) |
| Technical frames, keyframes, storyboard grids, or blockouts | [keyframes, storyboards, and blockouts](references/keyframes-storyboards-blockouts.md) |
| Observable performance, dialogue, audio, camera results, or conditional look | [performance, camera, and audio](references/performance-camera-audio.md) |
| Ambiguous camera terminology or a requested camera comparison | [camera movement reference](references/camera-movement-reference.md) |
| create/check/verbatim/scoped-revision boundaries and final delivery | [preservation and delivery](references/preservation-and-delivery.md) |
| Maintenance provenance or source reconciliation only | [source and change map](references/source-and-change-map.md) |

When source-ID conversion is needed for an editing or extension prompt, read only the source-ID mapping subsection in generation and references and keep the chosen video-task module as the owner. The source map and the frozen upstream document are maintenance evidence, not ordinary runtime prerequisites. Do not load a 92 KB donor or chain a second authoring skill for every request.

Reference-scope questions are conditional. Outside pure verbatim, if a request says only “use this reference” or “match this feeling” and the adopted attribute would change the result, inspect the readable reference relevant to that unresolved scope before formulating one necessary question about what should transfer, such as identity, set, action, camera, light, texture, or sound. Inspection informs the question; do not infer the user's desired transfer scope from the asset. If the reference is inaccessible, preserve user-established labels and roles in the prompt body and report the inspection limit outside it. Do not repeat a scope that the user already specified, answered, or delegated.

A caller-supplied **camera reference path** is optional. For **create**, **check only**, and **scoped prompt revision**, read that path only when the camera request is ambiguous, a camera comparison is requested, or the requested change needs movement terminology to be disambiguated. The text-operation label alone never triggers the read. Pure verbatim does not inspect or edit its payload. If a path or asset is inaccessible, retain any user-established label and role in the prompt body, and record the unknown status without pretending to inspect it.

## Authoring and delivery

After the guards and required references are loaded:

1. Preserve the protected contract.
2. For create or scoped revision, map each actually used reference to one explicit role and keep reference roles separate. For check only, inspect existing mappings without rewriting them. For verbatim, do not remap or inspect the payload.
3. Add observable action, camera result, sound, and state transitions only where the selected operation permits changes.
4. Keep platform parameters outside ordinary prompt prose unless the caller explicitly requires them as creative text. Never silently delete or redistribute authored time ranges.
5. Run the relevant checks in [preservation and delivery](references/preservation-and-delivery.md), then return the correct output kind.

Keep these surfaces distinct:

- **Prompt body**: complete text intended for copying into the next submission surface. It contains no internal analysis, review metadata, or reasons for edits.
- **Review or notes**: findings, assumptions, unresolved reference status, missing mandatory blocks, parameter notes, or capability limits outside the prompt body.
- **Submission-ready**: a complete prompt body that passed text-level preservation checks and has no unresolved required reference role or binding, master tag, parameter, or caller/project block for the intended surface. Text completeness alone is insufficient. This label still does not claim that assets are uploaded, slots are bound, a provider accepted the request, or media rendered.

When a caller asks for a prompt, include the complete body in the response. For a hybrid edit-plus-extension request, return sequential prompts labeled Step 1 and Step 2 and state that Step 2 uses Step 1's new master. Otherwise return one body by default. Do not append a generic quality pack, fixed look, negative list, hidden-cause reveal, or frame-precision promise.

## Final local check

Before delivery, confirm that the text operation and video task were kept separate, all protected facts and labels remain, inaccessible assets were not described as inspected, and no unrequested portion was rewritten. Confirm that the output kind matches create, check only, verbatim, or scoped revision; that review notes are outside the prompt; that required reference bindings, master tags, parameters, and caller/project blocks are resolved before using `submission-ready`; and that no execution, updater, installer, network, or media-generation action was introduced. For newly authored text or authorized revisions, inspect the exact copy payload for agent-added access/inspection/workflow, engine-routing/configuration, or execution-status notes; keep those outside while preserving model-facing tags, roles, scene directions, and caller-required parameters. This check does not authorize cleaning verbatim or protected original text.
