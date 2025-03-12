These are the things that happen *in-order* prior to out-of-order execution.

## High-Level Architecture of Front End

Branch prediction and fetch logic unit computes address of next instructions to be fetched.

These instructions are fetched from the instruction cache (I$).

Instructions are passed to decoder for turning into **instruction packets** (sometimes also called "backpacks").

![[High-level Front-end Arch.png]]

## Instructions and Cache Lines

Assume a fetch width of 4 and cache line size of 64B. Then four consecutive instructions can span up to two consecutive cache lines. But what if some of these instructions are branches? If we can't fetch the right instructions, we're just doing extra work for no reason and wasting time and cycles. We could use a better predictor.

## Branch Prediction

![[Branch Prediction]]

## Decode

![[Decode]]