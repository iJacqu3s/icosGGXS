## Making things shine
Glossy calculation is really similar to shadow calculation, in that it requires a dot product. For this, you will need the following inputs:
- The Incoming Vector (I)
- The Geometry Normal (N)
- The Light Direction (L)

Step 1: Scale the Incoming Vector (I) by -1
$$S^i=\text{scale}(I,-1)$$
Step 2: Reflect the Scaled Vector with the Object Normals (N) to get the Reflection Vector (Rv)[^1]
$$R^v=\text{reflect}(S^i,N)$$
Step 3: Apply the dot product between the Reflection Vector (Rv) and the Light Direction (L) to get the Roughness Range
$$\text{Range}=\text{dot}(R^v, L)$$
Step 4: Apply a power variable (G) to the Roughness Range to determine how large or small the roughness will be
$$\text{Gloss}=(\text{Range})^G$$

This returns an unclamped value that can be tweaked to increase or decrease the amount of area that is glossy. This can be done by changing the value of the power value (G)


[^1]: ![[Pasted image 20250219161449.png]]
