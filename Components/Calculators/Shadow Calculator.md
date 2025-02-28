## Making things shaded
To calculate shadows, you can use the dot product of the surface normals (N) and the direction of the main light (L).[^1]
$$
\text{Shadow = } \text{dot}(N,L)
$$
Typically, the main light is used to get the light direction[^2]. If the function fails, however, then you'll need to resort to creating a 3D vector to represent the XYZ rotation of the light.

The dot product returns an unclamped value range, which can be altered to increase or decrease the shadow area. You can use a remapping function to limit the range to a desired area.

[^1]: ![[Pasted image 20250219161640.png]]

[^2]: Unity Shader Graph Code:
	```
	#if SHADERGRAPH_PREVIEW
	    Direction = half3(0.5, 0.5, 0);
	    Color = 1;
	#else
	    Light light = GetMainLight();
	    Direction = light.direction;
	    Color = light.color;
	#endif
	```
