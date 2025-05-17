---
title: Writing a Raytracer in a Weekend
date: 24/1/25
tags:
  - computer-graphics
  - raytracer
---
## Creating the first image:
- For the first version of the code 
	- The pixels are written out in rows.
	- Every row of pixels is written out left to right.
	- These rows are written out from top to bottom.
	- Each of the red/green/blue components are repr internally by real-vars that range from 0.0 to 1.0. These need to scaled to integer values bw 0 and 255 before we print them out.
	- Red goes from fully off to fully on from left to right and green goes from fully off at the top to fully on at the bottom. Adding red and green light together makes yellow so we should expect the bottom right corner to be yellow.

### Adding a Progress Indicator 
- This is a handy trick to track the progress of a long render, and also to possibly identify a run that's stalled out due to an infinite loop or other problem.
- Our program outputs the image to the standard output stream -> so instead we write to the logging output stream.


### Vec3 Class:
- A class for storing geometric vectors and colors. 
- In many systems, these vectors are 4D(geometry + 1 vector for alpha transparency component for colors). For our purpose , three coordinates will suffice.
- use this same struct for colorrs, locations , directions ,offsets ,whatever -> for max code reuse.
- we will type alias vec3 into point3 and color. 

### color utility functions 
- with using our Vec3 class, we can create a new color header file and define a utility function that writes a single pixel's color to the std output stream.

## rays, simple camera and Background

### ray class:
- All ray tracers have is a ray class and a computation of what color is seen along a ray. Think of ray as a function $P(t) = A + tb$ .
- P is a 3D position along a line in 3D.
	- `A` is the ray origin 
	- `b` is the ray direction
	- `t` is a real number.
- We can repr the idea of ray as a class and repr the function `P(t)` as a function.

### sending rays into the scene:
- At its core, ray-tracer sends the rays through pixels and computes the color seen in the direction of those rays. Involved steps are:
	- Calculate the ray from the "eye" through the pixel.
	- Determine which objects the ray intersects 
	- Compute a color for the closest intersection point.
- Since we are targeting a non-square image, we'll choose a 16:9 because its so common. A 16:9 aspect ratio means that the ratio of the image width to image height is 16:9.
- Image's aspect ratio can be determined from the ratio of its width to its height. Since we have given a aspect ratio in mind, easier to set the image's width and the aspect ratio , and then using this to calculate for its height.
- This way, we can scale up or down the image by changing the image width, and it won't throw off our desired aspect ratio.
- Viewport is a virtual rectangle in the 3d world that contains the grid of image pixel locations.
-  why we don't just use `aspect_ratio` when computing `viewport_width`?
	- the value set to `aspect_ratio` is the ideal ratio, it may not be the _actual_ ratio between `image_width` and `image_height`. If `image_height` was allowed to be real valued—rather than just an integer—then it would be fine to use `aspect_ratio`. But the _actual_ ratio between `image_width` and `image_height` can vary based on two parts of the code. 
	- First, `image_height` is rounded down to the nearest integer, which can increase the ratio. Second, we don't allow `image_height` to be less than one, which can also change the actual aspect ratio.
	- `aspect_ratio` is an ideal ratio, which we approximate as best as possible with the integer-based ratio of image width over image height. 
- Camer Center:
	- A point in 3d space from which all scene rays will originate refererred to as the eye point. The vector from the camera center to the viewport center will be orthogonal to the viewport. 
- For simplicity, we have started with the camera center at (0,0,0,0). Also have the y-axis go up, the x-axis to the right and the negative z-axis pointing in the viewing direction.
- Inevitable tricky part:
	- While our 3D space has the conventions above, this conflicts with our image coordinates, where we want to have the 0th pixel in the top-left and work our way down to the last pixel at the bottom right. Meaning that our image coordinate Y-axis is inverted -> Y increases going down the image.

## Adding a Sphere:

#### Ray-Sphere Intersection
- Eqn for a sphere of radius r that is centered at the origin is an important mathematical eqn: $x^2 + y^2 + z^2 = r^2$
- If a given point $(x,y,z)$ is inside the sphere, then $x^2+y^2+z^2 < r^2$ and if a given point $(x,y,z)$ is outside the sphere, then $x^2+y^2+z^2 > r^2$.
- If we want to allow the sphere center to be at an arbitrary point (𝐶𝑥,𝐶𝑦,𝐶𝑧)(Cx,Cy,Cz), then the equation becomes a lot less nice: $(𝐶𝑥−𝑥)2+(𝐶𝑦−𝑦)2+(𝐶𝑧−𝑧)2=𝑟2$
- any point 𝐏P that satisfies this equation is on the sphere”. We want to know if our ray 𝐏(𝑡)=𝐐+𝑡𝐝P(t)=Q+td ever hits the sphere anywhere. If it does hit the sphere, there is some 𝑡t for which 𝐏(𝑡)P(t) satisfies the sphere equation. So we are looking for any 𝑡t where this is true: $(𝐂−𝐏(𝑡))⋅(𝐂−𝐏(𝑡))=𝑟2$ 

## Surface Normals and Multiple Objects:

#### Shading with Surface Normals
- surface normal -> vector that is perpendicular to the surface at the point of intersection.
	- If a unit length normal vector is ever required, then we might as well do it up front once, instead of over and over again for every location where unit-length is required.
	- We do require unit-length normal vectors in several places
	- If we require normal vectors to be unit length, then we can often efficiently generate that vector with an understanding of the specific geometry class, in the constructor of in the hit() function.
	- Sphere normals can be made unit length simply by dividing by the sphere radius, avoiding the equare root entirely.
- A common trick used for visualizing normals is to map each component to the interval from 0 to 1 , and then map (x,y,z) to (red,green,blue). For the normal, we need the hit point, not just whether we hit or not. 
- We have only sphere in the scene, and its directly in front of the camera, so we wont worry about negative values of t yet. Just assume the closest hit point(smallest t) is the one that we want. These changes in the code let us compute and visualize n.

#### Abstraction for Hittable Objects:
- Making a abstract class for anything a ray might hit, and make both a sphere and a list of spheres just something that can be hit. What that class should be called is something of a quandry -> calling an "object" would be good if not for "object-oriented" programming.
- hittable abstract class will have a hit function that takes in a ray. Most ray tracers have found it convenient to add a valid literal for hits tmin to tmax, so the hit only 'counts' if tmin < t < tmax. For the initial rays this is positive t, but as we see, it can simplify our code to have an interval tmin to tmax.

#### Front Faces Versus back Faces:
- Second design decision for normals is whether they should always point out. At present, the normal found will always be in the direction of the center to the intersection point(the normal points out). 
- If the ray intersects the sphere from the inside, the normal (which always points out,) points with the ray. Alternatively, we can have the normal always point against the ray.
- If the ray is outside the sphere, the normal will point outward, but if the ray is inside the sphere, the normal will point inward.
- We would need to choose one of them because we will eventually want to determine which side of the surface that the ray is coming from. This is important for objects that are rendered differently on each side, like the text on a two-sided sheet of paper,or for objects that have an inside and an outside, like glass balls.
- To determine, which side the ray is on when we color it -> figure this out by comparing the ray with the normal. If the ray and the normal face in the same direction, the ray is inside the object, if the rat and the normal face in the opposite direction, then the ray is outside the object. 
- We can set things up so that normals always point "outward" from the surface,or always points against the incident ray. This decision is determined by whetehr we want to determine the side of the surface at the time of geometry intersection or at the time of coloring. 

#### A list of hittable objects:
- Add a new class that stores a list of hittables -> based on the generic objects called a hittable.
- 