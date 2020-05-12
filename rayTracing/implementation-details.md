# Ray Tracing - Implementation Details

## Method Used

A recursive function is used to simulate the branching of rays after collision with surfaces. The pixel color value depends on a weighted sum of color values generated by each ray-mesh intersection. The weights depend on the properties of the mesh surface. Desired materials can be generated by defining these properties appropriately.

### Diffuse Lighting

The project demonstrates 2 types of lights, point and directional lights. Lighting at point is calculated as follows:

- A ray is cast from the ray-mesh intersection point towards the light source (for directional lights, this will be in a direction opposite to the direction of light).

- If the ray does not intersect with any mesh, before reaching the light source (for direction lights, this will be at infinity), the the surface point is lit by the light.

- Since the surfaces implemented as perfectly diffuse, color calcluation are easy.

![Sample image](imagesGenerated/scene0_after_normalization.png)

### Ray Mesh Intersection Calculation

Since the intersection msut be calculated with millions of rays, a structure (refered to as the collTriangle in this project) is initialized to represent each triangle and accelerate intsersection calculations.

This structure contains the mathematical description of the plane of the triangle (a point and a normal), and 3 planes perpendicular ot the triangle containing the sides of the triangle.

The plane of the triangle is used to calculate the ray-mesh intersection and the other 3 side planes are used to check whether the intersection is inside the triangle or not.