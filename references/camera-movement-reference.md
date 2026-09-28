# Camera Movement Reference

This is a compact, engine-neutral, conditional lookup for camera terms. Consult only when the user's movement is ambiguous, two candidate terms need comparison, the physical path is important, or the user asks for a reference. A clear explicit instruction or a sufficient camera reference takes priority. Looking up a term does not authorize a rewrite of an otherwise clear request, including a `check only` or local camera revision.

## A small writing grammar

Use only the fields the shot needs:

```text
target + physical starting position + movement/path + direction + arrival composition or state
```

Add speed, focus, parallax, or a settling hold only when the caller needs that visible result. `centered`, `constant speed`, `smooth`, and `settle` are optional descriptors, not global defaults. This reference is vocabulary, not an allowed-move whitelist, an engine support claim, or a mandatory prompt schema. It does not copy all source entries or require a fixed number of fields.

## Distinction pairs

| Pair | First term | Second term | Choose by the visible change |
|---|---|---|---|
| **Pan / truck** | Rotate horizontally about a fixed pivot. | Translate the camera laterally while the lens direction stays aimed. | Pan changes view around a pivot; truck creates lateral parallax and a new physical position. |
| **Truck / slider** | A general lateral camera translation through space. | A short, constrained rail or slider travel; it can perform a truck but the rig name alone does not define the path. | Both can create lateral parallax. State the physical path and endpoint; do not infer a rigid trajectory from `slider` or treat `truck` as a fixed rig. |
| **Tilt / pedestal** | Rotate vertically about a fixed pivot. | Translate the whole camera vertically with the lens direction held. | Tilt changes the view angle; pedestal changes camera height while keeping the optical direction. |
| **Zoom / dolly** | Change focal length; perspective relationships stay optically framed. | Move the camera toward or away from the subject; perspective and parallax change. | Use zoom for scale without a physical approach; dolly for a real spatial approach or retreat. |
| **Dolly / push** | Physical forward or backward travel. | A short forward or backward dolly described as a gradual emphasis or release. | `Push` is a writing shorthand; specify physical travel when perspective matters. |
| **Arc / orbit** | Shallow curved travel around part of a subject. | A circular path around a subject at an intended radius. | Arc changes angle over a partial path; orbit implies a more sustained circle. |
| **Pan / arc** | View rotates without changing camera position. | Camera position travels on a curve, changing parallax and angle. | Ask whether foreground/background separation must reveal a physical move. |
| **Crane / pedestal** | Broad vertical travel through open space, often changing scale or elevation. | Straight vertical translation with the lens pointed in the same direction. | Crane can include an aerial rise or descent; pedestal is a constrained vertical lift/drop. |
| **Tracking / follow** | General movement that keeps pace with a moving subject. | Follow from behind along the subject's route, often with back/shoulder as guide. | Use the relation to the subject and route, not the label alone. |
| **Reverse tracking / side tracking** | Camera moves backward in front of a subject. | Camera moves parallel beside the subject. | Front-facing approach versus profile or three-quarter parallel travel. |
| **Low tracking / vehicle tracking** | Track at ground or below-waist height, matching feet or wheels. | Move with a vehicle along its route. | Choose the tracked object and height that must remain readable. |
| **Chase / tracking** | Reactive pursuit that may reframe around the action. | Deliberate subject-following movement with a stable relation. | Chase implies action pressure only when the user requests it; do not infer it from movement alone. |
| **Rack focus / zoom** | Shift sharpness between depth planes. | Change image scale through focal length. | Focus change is a depth-of-field event; zoom is a scale event. |
| **Roll / Dutch angle** | Rotate the camera around its optical axis. | Tilt the whole frame's horizon as a composition choice. | Use the requested roll or canted result; do not assume a roll from a tense mood. |
| **Push past / pass-through** | Move forward past a foreground object or edge. | Continue through a visible opening into the space beyond. | A physical doorway or gap differs from an explicitly requested solid-surface effect. |

## Tracking and rig snippets

These are short role definitions, not full prompts:

- **Follow behind:** camera travels behind the subject at the route's pace; the shoulder, back, or head guides the foreground and the path ahead remains readable.
- **Reverse tracking:** camera retreats in front of the subject; preserve a front-facing relationship while the background moves behind.
- **Side tracking:** camera translates parallel to the subject; preserve side or three-quarter profile and the direction of travel.
- **Low tracking:** camera stays near the ground; keep feet, wheels, or the requested lower detail readable against the moving ground plane.
- **Vehicle tracking:** camera travels with the vehicle; keep the vehicle stable while the route passes.
- **Chase:** camera follows the action route with the requested reactive reframing; specify how much subject loss or shake is allowed.
- **Snorricam/body-mounted:** camera is fixed relative to the subject's torso or face while the background moves around the subject; state whether the subject remains close and centered.
- **Handheld:** camera is held at a human operator position with the requested sway or micro-adjustment; it does not imply a particular lens, speed, or framing.
- **Steadicam/gimbal:** camera glides with the specified subject or route; the rig name does not decide the path or endpoint.
- **First-person:** camera occupies the character's viewpoint; use visible hands, arms, or body edges as the physical viewpoint anchor when needed.
- **Drone/aerial:** camera travels through open space at an explicit height and direction; state the destination scale and the ground or horizon relationship.

## Five control families

Classify the requested change before combining labels:

1. **Physical rotation:** pan, tilt, roll, and canted angle rotate the camera about a pivot or optical axis.
2. **Physical translation:** dolly, truck, pedestal, crane, arc, orbit, tracking, pass-by, and aerial travel move the camera through space.
3. **Optical/focus:** zoom, crash zoom, focal-length change, rack focus, and depth-of-field changes alter the image optically; they do not automatically move the camera.
4. **Rig/viewpoint:** handheld, Steadicam, gimbal, body-mounted/Snorricam, first-person, vehicle, and drone describe the camera's relation to an operator, subject, or vehicle. They still need a path and endpoint when movement matters.
5. **Time/compositing:** time-lapse, slow motion, speed ramp, bullet-time, freeze-frame, object wipe, light wipe, mask, morph, and through-object effects alter temporal or layered continuity. They do not become physical camera moves by name alone.

Compound directions are mixable when each phase has a reason and a visible endpoint: for example, “truck right past the foreground post, then pan right to keep the actor in the arrival composition.” Do not add a compound move merely to sound cinematic.

## End-state examples

```text
Pan right: begin on the seated subject from the fixed doorway position, rotate horizontally to the right with the horizon level, and end with the window fully readable beside the subject.

Truck right: begin at the table's near-left side, translate the camera right while keeping the lens aimed along the table so foreground and background show parallax, and end on the doorway.

Zoom in: keep the camera position and perspective fixed while the focal length narrows toward the letter, and end with the letter readable in a tighter frame.

Dolly in: move the camera physically toward the subject along the room axis, preserving the approach perspective, and end at the requested medium close-up.

Static camera: keep the camera fixed at the stated position and composition while the subject, light, and sound continue; end on a live stable hold.

Frame hold after movement: complete the stated pan, truck, or dolly, stop the camera at the arrival composition, and let the requested live action continue.

Frozen frame: stop image motion at <requested moment>; use only when the user asks for a freeze.

Multi-keyframe: bind the actual first, middle, and last states through the supported input roles; a prose “first” or “last” sentence alone does not guarantee slot binding.

Pass-through: approach the visible doorway centered in frame, continue through the opening, and end inside the next space; if the user wants a solid wall to behave as a portal, name that as a compositing effect.
```

Use `fast`, `slow`, or another speed word according to the requested result and caller policy. This reference does not impose a global speed blacklist. A speed descriptor never replaces the path, target, or arrival state.

## When to stop looking up terms

Do not consult this file when the user has already supplied a clear movement, a sufficient physical camera reference, or a pure verbatim request. Do consult it when “move left,” “reverse,” “track,” “zoom,” or “through” could produce materially different camera geometry; when pan and truck, zoom and dolly, or stable and frozen are being confused; or when a local camera-only revision must preserve every other attribute. After lookup, write the smallest request-scoped change and leave unrelated wording untouched.

This reference is maintained as a compact derivative of the camera source. The source's category count and examples are provenance, not a claim about Seedance support, a prompt limit, or a runtime dependency.
