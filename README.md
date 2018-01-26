# CIS 566 Project 1: Noisy Planets


Name: Alexis Ward

PennKey: aleward

External Links:

- I used the Simplex 3D Noise function from: https://gist.github.com/patriciogonzalezvivo/670c22f3966e662d2f83 (Myles told me about this link)
- I used the following function to help me compute rotation matrices: http://www.neilmendoza.com/glsl-rotation-about-an-arbitrary-axis/

Screenshots: (in repository)

![](ss1.png)
![](ss2.png)
![](ss3.png)
![](ss4.png)
![](ss5.png)
![](ss6.png)

Explanation:

My scene is composed of three renderings of the same icosphere. One is used for the moon, one is used for the center planet, and one is used for the clouds surrouding the planet.

I used Simplex noise for almost all effects in this project. For the moon's vertex shader, I sampled the noise at 4 different octaves, sqaure rooted the resulting float multiple times, and set a cut-off value; this resulted in a smooth sphere with many sharp craters. Its fragment shader maps colors to new noise values (as well as noise values sent from the vertex shader), and implements slight Blinn Phong shading sepending on the surface color.  For the planet's vertex shader, I sampled the noise at 6 different octaves, and then cut it off at a value fluctuating between 0 and about 1/15 to make water look as if it's expading and contracting. In it's fragment shader I calculated the noise in different ways for the water, sand, and ground features. The water has a Blinn Phong shine at the brighter stripes to simulate cresting waves, and the ground has darker patches in the light based on Blinn Phong as well. I only use the cloud vertex shader to scale the icosphere, and it's fragment shader uses maps simple noise to semi-transparent surface.

I also computed the deformed normals in both the moon and planet vertex shaders. I approximated hypothetical points on the sphere close to each vertex in question, calculated their deformations, and took the cross product (of the vectors between the vertex and the hypothetical points). Several different cases are laid out in the shader to avoid mathematical error.

Additionally, the planetary motions are all handled in the CPU.


## Objective
- Continue practicing WebGL and Typescript
- Experiment with noise functions to procedurally generate the surface of a planet
- Review surface reflection models

## Base Code
You'll be using the same base code as in homework 0.

## Assignment Details
- Update the basic scene from your homework 0 implementation so that it renders
an icosphere once again. We recommend increasing the icosphere's subdivision
level to 6 so you have more vertices with which to work.
- Write a new GLSL shader program that incorporates various noise functions and
noise function permutations to offset the surface of the icosphere and modify
the color of the icosphere so that it looks like a planet with geographic
features. Try making formations like mountain ranges, oceans, rivers, lakes,
canyons, volcanoes, ice caps, glaciers, or even forests. We recommend using
3D noise functions whenever possible so that you don't have UV distortion,
though that effect may be desirable if you're trying to make the poles of your
planet stand out more.
- Implement various surface reflection models (e.g. Lambertian, Blinn-Phong,
Matcap/Lit Sphere, Raytraced Specular Reflection) on the planet's surface to
better distinguish the different formations (and perhaps even biomes) on the
surface of your planet. Make sure your planet has a "day" side and a "night"
side; you could even place small illuminated areas on the night side to
represent cities lit up at night.
- Add GUI elements via dat.GUI that allow the user to modify different
attributes of your planet. This can be as simple as changing the relative
location of the sun to as complex as redistributing biomes based on overall
planet temperature. You should have at least three modifiable attributes.
- Have fun experimenting with different features on your planet. If you want,
you can even try making multiple planets! Your score on this assignment is in
part dependent on how interesting you make your planet, so try to
experiment with as much as you can!

For reference, here is a planet made by your TA Dan last year for this
assignment:

Notice how the water has a specular highlight, and how there's a bit of
atmospheric fog near the horizon of the planet. This planet used only simple
Fractal Brownian Motion to create its mountainous shapes, but we expect you all
can do something much more exciting! If we were to grade this planet by the
standards for this year's version of the assignment, it would be a B or B+.

## Useful Links
- [Implicit Procedural Planet Generation](https://static1.squarespace.com/static/58a1bc3c3e00be6bfe6c228c/t/58a4d25146c3c4233fb15cc2/1487196929690/ImplicitProceduralPlanetGeneration-Report.pdf)
- [Curl Noise](https://petewerner.blogspot.com/2015/02/intro-to-curl-noise.html)
- [GPU Gems Chapter on Perlin Noise](http://developer.download.nvidia.com/books/HTML/gpugems/gpugems_ch05.html)
- [Worley Noise Implementations](https://thebookofshaders.com/12/)


## Submission
Commit and push to Github, then submit a link to your commit on Canvas.

For this assignment, and for all future assignments, modify this README file
so that it contains the following information:
- Your name and PennKey
- Citation of any external resources you found helpful when implementing this
assignment.
- A link to your live github.io demo (we'll talk about how to get this set up
in class some time before the assignment is due)
- At least one screenshot of your planet
- An explanation of the techniques you used to generate your planet features.
Please be as detailed as you can; not only will this help you explain your work
to recruiters, but it helps us understand your project when we grade it!

## Extra Credit
- Use a 4D noise function to modify the terrain over time, where time is the
fourth dimension that is updated each frame. A 3D function will work, too, but
the change in noise will look more "directional" than if you use 4D.
- Use music to animate aspects of your planet's terrain (e.g. mountain height,
brightness of emissive areas, water levels, etc.)
- Create a background for your planet using a raytraced sky box that includes
things like the sun, stars, or even nebulae.
