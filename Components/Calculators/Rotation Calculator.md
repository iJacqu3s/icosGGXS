# Getting the Rotation
In my opinion, this is the most complex part of the whole system, since it isn't a very easy problem to solve for someone who doesn't do programming.

In Blender, this is usually solved via a driver that gets the rotation from the main light[^3]. The same for the Object. But in Unity, and I suspect other engines, it isn't so simple.

In Unity, you need to use a transformation matrix[^1]. This gets the Object's Rotation (O) in radians, which you can then subtract from the Light Direction's X value (X).

From there, the process goes as follows:

Step 1: Range mapping - divide O by Pi

$$O^m=\frac{O}{\pi}$$

Step 2: Calculate the Rotation Interference (RI)

$$RI = \frac{ X - O^m}{2}$$

Step 3: Repeat the range[^2]

$$\text{Range}=\text{frac}(RI)$$

Step 4: Flip Logic - Greater than (B1), Less than (B2) - The Flip Boolean (U) decides whether the U coordinates of the image's UVs get flipped or not

$$\text{B1}=\text{bool}(\text{Range}>0.5)$$

$$\text{B2}=\text{bool}(\text{Range}<0.5)$$

$$\text{U}=\text{B1}-\text{B2}$$

Step 5: Remap Shadow Map range - This creates a hard toon-like cutoff point

$$\text{Abs}=\text{absolute}(\text{B2 }-\text{Range})$$

$$\text{Remap}=\text{bool}(\text{Shadow Map }>\text{Abs})$$

![Current Graph Prototype](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/images/Pasted%20image%2020250219162359.png>)
![Transformation Matrix](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/images/o4b3hlg.jpg>)

[^1]: Getting an object's rotation in Shader Graph : https://discussions.unity.com/t/shadergraph-how-do-i-get-an-objects-rotation-value-inside-of-shadergraph-hdrp/246378/2

[^2]: Fraction Function : This function takes a range, and repeats it from 0 to 1. Any values outside that range gets discarded. From : https://blender.stackexchange.com/questions/159223/what-does-the-fraction-math-node-do

[^3]: Remember to divide the light rotation by π
