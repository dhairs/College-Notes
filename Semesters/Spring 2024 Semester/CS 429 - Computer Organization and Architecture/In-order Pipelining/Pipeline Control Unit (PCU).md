## What is it
The pipeline control unit defines global behavior for the pipeline, ensuring that instructions are either bubbled or stalled when necessary.
## Events

A boolean value that indicates that a certain hazard condition is imminent

Def-use and non-back-to-back load-use cases are handled using forwarding, so the PCU doesn't have to get involved.

Remaining situations
- Back-to-back load-use
	- `X_out-op == OP_LDUR && ((X_out->dst == src1) || (X_out->dst == src2))`
- Mis-predicted conditional branch
	- `X_out->op == OP_B_COND && !M_in->cond_holds`
- Handing `ret`
	- `D_out->op == OP_RET`

## Actions

Back-to-back load-use (*bubble for stalling*)
- (F, D, X, M, W) = (Stall, Stall, Bubble, Normal, Normal)

Mis-predicted conditional branch (*bubble for squashing*)
- (F, D, X, M, W) = (Normal, Bubble, Bubble, Normal, Normal)

Handling `ret` (*bubble for stalling*)
- (F, D, X, M, W) = (Stall, Bubble, Normal, Normal, Normal)

