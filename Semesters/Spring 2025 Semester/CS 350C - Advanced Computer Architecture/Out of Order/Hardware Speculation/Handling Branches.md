## Handling Branch Mispredictions

Recall that [[Branch Prediction|branch prediction]] runs well ahead of branch resolution. When a branch is resolved, result needs to be fed back to the branch predictor (located in the front end) so that it can update its tables. The front end needs to get the PC and whether or not the branch was resolved. 


> [!faq] What information needs to be communicated to the front end?
> This can also be a race condition, if the branch predictor is predicting and also 
> updating the tables. It is good to prioritize the update so that you can have more
> accurate predictions for the next branch.

If branch prediction and resolution disagree, then additional actions need to be taken to restart fetch from correct target, allow OOO core to drain, flush ROB, etc.
- We need to clear the instruction fetch (IF) queue. 
- Then, we need to flush the OOO core.

![[OOO IF Queue flushing.png]]

To be able to handle stuff like this, we need a very strict exception model. Branch mispredictions are faults, so we need a way to [[Handling Faults|handle faults]].