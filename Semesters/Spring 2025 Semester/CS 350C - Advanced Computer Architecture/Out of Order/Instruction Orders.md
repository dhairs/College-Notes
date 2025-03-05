
## Which dependences need to be respected?

| Type                  | Needs to be respected? |
| --------------------- | ---------------------- |
| Program Order         | No                     |
| Data (RAW) Dependence | Yes                    |
| Control Dependence    | No                     |
| Name Dependences      | WAR: No<br>WAW: No     |

You'll notice that RAW is the only one you truly have to respect because it is data dependence and affects program correctness.

## Removing <u>Name</u> Dependences

These dependences only occur because we have a finite number of **architectural** registers. They are called 'name' dependences because we have to write to the same named register. 

If we went to get rid of this type of dependence, we could possibly map registers to a different space. The tradeoff in this case is you have to maintain the mappings of each register and instruction and do bookkeeping. 

## Subtleties in Write-Back

At the architectural level, it should not be possible to observe whether the processor is in-order or out-of-order. This must hold **even** in the presence of an exception or interrupt.

We need to be able to provide **precise exceptions** and **precise interrupts**.