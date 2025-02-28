## Inputs
- Detail Map (RBG) (A)
- Detail Highlight Mask (Mask)
## Operations
Isolate Highlights:
- In (A, Mask)
- Blend (factor:Mask) (slot-a:0) (slot-b:A)
- Out (Highlight Mask)
Isolate Details:
- In (A, Mask)
- Blend (factor:Mask) (slot-a:A) (slot-b:0)
- Out (Detail Mask)
## Outputs
- Highlight Mask (dhm)
- Details Mask (ddm)