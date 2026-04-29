# Shaping Actions

Use these actions as prompts during shaping. They help decide what to investigate next, but they do not define a required sequence. Use one action or combine several when that best advances the R/J/S model.


## Generate Alternative Shapes or Components

Prompts:

- What radically different architecture could work?
- What component could be removed?
- What is the simplest functioning shape?
- Are we using existing libraries or vendors well?

If alternatives involve unfamiliar technology, check primary documentation before leaning on assumptions.

## Generate Alternative Journeys

Prompts:

- What parts of the journey may be overly complex? What are our options to simplify them?
- What would be the simplest version of this journey? 
- What would it mean to shift some responsibility from the actor to the system or from the system to the actor? Does it unlock new shape directions?
- What would it mean to prevent the user from having through that journey?

## Challenge The Baseline

Prompts:

- How does the current system shape constrains our exploration? 
- Are these constraints actual requirements? And if so how necessary are they?
- What new tradeoffs may become available if we were to drop some of these constraints?

## Run an Adversarial Review

Review the shaping document with fresh eyes looking for:
- Reasonning/logic gaps
- Undocumented assumptions about the shape, its components, the actors, the constraints...
- Intrinsic knowledge is being relied on.

## Run Fit Check

Run a fit check to identify gaps between R, J and S:
- Which requirements lack a corresponding journey or shape component?
- Which shape components lack a requirement?
- Which journey requires a system behaviour that the shape does not fullfil?

## Slice Early

Use when slicing may expose hidden tradeoffs or excessive scope.

Early slicing is exploratory. If the user asks to slice and it is unclear whether they mean exploratory slicing or final slicing, ask which mode they want. Final slicing requires the user to confirm that the shape is final.
