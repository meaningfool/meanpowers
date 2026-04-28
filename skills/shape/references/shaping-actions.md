# Shaping Actions

Use these actions inside the main shaping loop. After applying an action, work through the result with the user and update R/J/S until the model is internally consistent.

## Refine Requirements

Use when requirements are vague, solution-shaped, missing, or disputed.

- clarify the outcome
- remove solution details from R
- split compound requirements
- mark status changes explicitly
- check consequences for journeys and shapes

## Generate Alternative Shapes

Use when the current shape feels too narrow or complex.

Prompts:

- What radically different architecture could work?
- What component could be removed?
- What is the simplest functioning shape?
- Are we using existing libraries or vendors well?

If alternatives involve unfamiliar technology, check primary documentation before leaning on assumptions.

## Refine A Shape Component

Use when a component is flagged or underspecified.

- generate concrete options
- identify mechanics that need investigation
- decide whether to spike
- update requirements and journeys if the component changes the product shape

## Generate Alternative Journeys

Use when actor responsibilities or workflows are unclear.

- shift responsibility between actor and system
- make the journey simpler
- consider a different actor
- identify requirements implied by the new journey

## Challenge The Baseline

Use when the existing system silently imposes constraints.

- identify inherited requirements
- ask whether they still matter
- surface tradeoffs between keeping, dropping, or changing them

## Adversarial Review

Use when the shape seems converged but may hide assumptions.

- what gaps are silently filled by assumptions?
- what intrinsic knowledge is being relied on?
- which requirements lack a corresponding journey or shape component?
- which shape components lack a requirement?

## Slice Early

Use when slicing may expose hidden tradeoffs or excessive scope.

Early slicing is exploratory. If the user asks to slice and it is unclear whether they mean exploratory slicing or final slicing, ask which mode they want. Final slicing requires the user to confirm that the shape is final.
