This is the documentation for a custom shader named "icosGGXS". 

The goal of this shader is to replicate certain elements of the Guilty Gear XRD and Strive style, whilst having an identity of its own and maintaining a similarity to the original reference artworks that have been provided.
## Shader Functions
For the purposes of simplification and ease of use, the icosGGXS shader will be comprised of several smaller components. For the purposes of this document, the following terms hold the following definitions:
- Calculator - a function that computes an output that can be utilised later on for general purposes.
- Operator - a function that takes an input, such as a texture map, vertex colour, etc, and returns an output that can be used to achieve specific effects.
### Calculators
For the GGXS shader, there are three main calculators that provide the necessary inputs for the shader to function.

| Calculator              | Function                                                                                             |
| ----------------------- | ---------------------------------------------------------------------------------------------------- |
| [Shadow Calculator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Calculators/Shadow%20Calculator.md>)   | Computes a clamped value between 0 and 1 to represent the shaded geometry.                           |
| [Glossy Calculator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Calculators/Glossy%20Calculator.md>)   | Computes a clamped value between 0 and 1 to represent the highlights or shiny parts of the geometry. |
| [Rotation Calculator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Calculators/Rotation%20Calculator.md>) | Computes a 4D Matrix that is deconstructed to determine the object's global rotation.                |

### Operators
These are the functions that make the geometry actually look presentable. There are quite a few operators that make the shader tick. 

| Operator                          | Function                                                                                                                                          |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Colour Map Operator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Operators/Colour%20Map%20Operator.md>)           | Takes the colour and shadow textures, and extracts the outlines to be used as a mask later on.                                                    |
| [Detail Map Operator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Operators/Detail%20Map%20Operator.md>)           | Takes the detail texture and extracts an alpha value from the RGBA input to be used as a mask later on.                                           |
| [Fresnel Operator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Operators/Fresnel%20Operator.md>)              | Takes the input masks and removes or adds the masked areas from the Fresnel values.                                                               |
| [Fresnel Outline Operator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Operators/Fresnel%20Outline%20Operator.md>)      | Takes an input mask and width value and creates an outline based on Fresnel.                                                                      |
| [Normal Map Operator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Operators/Normal%20Map%20Operator.md>)           | Takes a normal map input and modifies the geometry normals accordingly, which can then be sent to the [[Shadow Calculator]].                      |
| [Shadow Operator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Operators/Shadow%20Operator.md>)               | Takes an input from the [[Vertex Colour Operator]] output and [[Shadow Calculator]] output and clamps it to a desired range.                      |
| [Shadow Map Operator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Operators/Shadow%20Map%20Operator.md>)           | Takes a shadow map and [[Rotation Calculator]] output as input to calculate a show that is not based on an object's normals.                      |
| [Shine Map Operator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Operators/Shine%20Map%20Operator.md>)            | Takes inputs from a detail map, shine mask, and [[Glossy Calculator]] to display a custom highlight/shine.                                        |
| [Transparency Operator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Operators/Transparency%20Operator.md>) | Takes an input from a transparency map and creates an output to determine object transparency with either a hard cutoff or a soft / blended fade. |
| [Vertex Colour Operator](<https://github.com/iJacqu3s/icosGGXS/blob/main/Components/Operators/Vertex%20Colour%20Operator.md>)        | Takes a vertex colour as input and outputs a series of 4 masks based on RGBA values.                                                              |

### Shadow Operator vs Shadow Map Operator
These two systems are not compatible with each other, seeing as one uses geometry normals to calculate shadows, and the other uses a shadow map texture and object rotation.
