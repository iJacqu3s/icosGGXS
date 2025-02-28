## Inputs
- Outline Mask (tom) *from [[Colour Map Operator]]*
- Shaded Area (sa) *from [[Shadow Operator]]*
- Fresnel Mask (fmask) *from [[Vertex Colour Operator]]*
- Minimum (min)
- Maximum (max)
- Switch (switch)
## Operations
Compute Fresnel:
- Fresnel Layer Weight (out:Facing)
- Out (Facing)
Exclude Outlines
- In (Facing) (tom)
- Multiply (Facing) (tom) (out:F1)
- Out (F1)
Exclude Areas From Rimlight
- In (F1) (sa)
- Change Interpolation (Linear:sa)->(Ease:sa1)
- Blend Multiply Clamped (factor:1) (slot-a:F1) (slot-b:sa1) (out:F2)
- Multiply Clamped (F2) (fmask) (out:F3)
- Remap (F3) (from:min,max) (to:0,1) (out:F4)
- Blend (factor:switch) (slot-a:0) (slot-b:F4)
- Out (Fresnel)
## Outputs
- Fresnel (fresnel)