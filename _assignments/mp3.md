---
layout: assignment
title: "MP3: Environment Mapping"
index: 10
due: "Nov. 20, 2020 @ 11:59 PM"
material: ~
points: 15
rubric:
  -
    name: Runs and renders
    points: 1
    description: Program runs without crashing and renders visible polygons.
  -
    name: Commented
    points: 1
    description: Each function in your code is commented in the required style.
  - 
    name: Load OBJ File
    points: 1
    description: Load and render the geometry of the Teapot OBJ correctly.
  -
    name: London Skybox and Cubemap
    points: 2
    description: Render a skybox texture mapped using the 6 images from the cube map.
  - 
    name: Orbit
    points: 2
    description: Implement the ability for users to orbit around the teapot.
  - 
    name: Unique Skybox and Cubemap
    points: 2
    description: Allow users to switch to viewing a scene that uses a cubemap you created.    
  - 
    name: Shading
    points: 2
    description: Shading is accomplished using the the Phong reflection model in the fragment shader.
    
  - 
    name: Reflection
    points: 2
    description: Allow users to switch to viewing a cube-mapped reflective teapot.
 
  -
    name: Refraction
    points: 2
    description: Allow users to switch to viewing a cube-mapped refractive (glass) teapot.
---

![teapot](/img/teapot.png)  
Your goal is to write an app that loads the Utah teapot from a file and renders it. 

Your app should have the following features:

+ Rendered in perspective
+ A skyboxed scene that can can be switched between:
  1. A London street [images provided below](https://illinois-cs418.github.io/assignments/mp3.html#london-skybox)
  2. A scene you capture using a camera and convert into a cubemap [instructions below](https://illinois-cs418.github.io/assignments/mp3.html#your-own-skybox)
+ Allow the user view to orbit around the teapot.
+ A control in the HTML that allows the user to switch between
  1. simply shading the teapot
  2. making the teapot reflective
  3. making the teapot refractive

+ Your code should use a cubemap for the required texture effects.
  1. Reflection on the teapot should always be consistent with the scene rendered on the skybox.
  2. When using the cube map on the teapot, you do not have to also use Phong reflection. 

Your app should look something like the image above.

## How to Work on the MP ##

You should work on the MP incrementally. Test each piece before moving on. Start now.
Here's a suggested plan of attack:
+ Week 1: Implement the skybox and cubemap and orbit.
1. Create a mesh of a cube using 12 triangles centered at origin. Test.
2. Add the cube map and move the view inside the cube to see the skybox. Test.
3. Add in the ability to orbit the view inside the skybox around the origin. Test.
+ Week 2: Implement reader for the teapot and reflective shader and rotation
1. Incorporate the OBJ reader code to load the teapot. Test.
2. Implement phong shader for the teapot. Test
3. Add a reflective shader for the teapot. Test.
+ Week 3: Implement phong shader and refractive shader
1. Implement refraction. Test.
2. Capture your own cubemap and the ability to swicth the scene to use it. Test


## Multiple Shaders ##
You should implement more than one shader program for this MP. At a minimum, it makes sense to have separate shaders for the teapot and skybox. You could break it down even further and have three shader programs for the teapot (Phong, reflective, and refractive). **Be very careful if you cut and paste code when doing this.** In given code using single shaders, lots of information, e.g. location of attributes in the shader program, is stored as attributes of the program object. You will need to handle these correctly for each shader program.


## London Skybox ##
Create and draw an environment using skyboxing...render a large cube surrrounding the viewer...this is the skybox. Use the cube map images to texture map the inside of the skybox. **Just to be clear, instead of texture mapping each side of the skybox independently, you should use the cubemap...you just have to figure out what direction vector to use when accessing the environment map to color a fragment on the box.**


### Background Reading and Resources ###
 + A set of 6 image files forming a cubemap are available in this [zip file](https://github.com/illinois-cs418/illinois-cs418.github.io/raw/master/img/London.zip). You can use these for the MP if you wish.
 
+ A good tutorial about using cube maps is available from [webglfundamentals.org](https://webglfundamentals.org/webgl/lessons/webgl-environment-maps.html)

## Your Own Skybox ##
 
You can make your own cubemaps as well. Here's a how to do it:
1. Capture a photo sphere of a scene using a phone camera and Google Street View using these [instructions](https://support.google.com/maps/answer/7012050?co=GENIE.Platform%3DAndroid&hl=en). This should work on either android or iphone. There are some tips on how to do this well [here](https://www.lifewire.com/what-is-android-photo-sphere-1616136).
2. Convert the Photo Sphere images to 6 cubemap images. You can use any of the following options:
+ Use [this site]()
+ Use [this site](http://pano.sentiovr.com/)
+ Do it yourself using code...check out [this stackoverflow post](https://stackoverflow.com/questions/29678510/convert-21-equirectangular-panorama-to-cube-map).

This does not have to be perfect. There will be some artifacts in your images, and that's fine. 

## Teapot Mesh ##
You can grab an OBJ file containing the famous Utah Teapot Mesh [here](https://github.com/illinois-cs418/cs418CourseMaterial/raw/master/Meshes/teapot_0.obj).

### Background Reading and Resources ####

The OBJ file format is documented in this [wikipedia article](https://en.wikipedia.org/wiki/Wavefront_.obj_file).
You will need to get the OBJ file from the server, and then parse it to generate the vertex and face arrays. You can reuse code you completed for the in-class lab exercise on meshes.

If you didn't do the exercise, you can use the function given in [readText.js](https://github.com/illinois-cs418/cs418CourseMaterial/raw/master/CodeExamples/readText.js) to get a file and send it to the function you will write to parse the file.

Use the above linked teapot model, which consists only of vertices and triangular faces. Load the vertices into a vertex position array, and the triangle faces into a face array whose elements are triples of vertex indices. **Note that the indices of the vertices in the OBJ start at 1**. This means you will need to adjust them assuming your arrays start indexing at 0. You will need to create per-vertex normals for the mesh as well, which you should compute as the average normal of the the trangles incident on the vertex.

### Running a Local Server ###
To get around the issue of reading files from the local filesystem, it is best to test by running a local webserver. There are two relatively easy ways to do this:

+ If you use the Brackets editor, the live preview function will start up a server (and browser) to test your code. Just have Chrome open, and the open your html file in Brackets. Click the lightning bolt icon in the top right of the Brackets window.

+ Alternatively, you can install [node.js](https://nodejs.org/en/) Then install and run [httpserver](https://www.npmjs.com/package/httpserver) to serve the directory that it is run from.

## User Interface ##
Your user interface should alllow to the user view to orbit the teapot (just letting the view circle the teapot by rotating around the y-axis is fine, it needn't employ quaternions). This effect can be achieved by rotating the world (teapot and enclosing environment box) assuming the teapot is at the origin. Or you can implement it as part of the view tranformation. 

## Lighting ##
Use a point light source to light the model from the direction (1,1,1). You can adjust the ambient light as you wish, but it must be possible to see the effects of diffuse shading and a specular highlight on the teapot. Use Phong reflectance model and Phong shading.

## Comment appropriately ##

You should comment each file with an author comment and comment each function you write with a header. Use JSDoc comments with the appropriate tags and types.
Details can be found in the Google JavaScript Style Guide. 
