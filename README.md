# Softbodies
Softbodies, Jiggly items and other slimy stuff in Unity

## Description

This is an exploration of an idea of making dynamic, jelly-like meshes. Those objects are always a nice addition to a interactive world.
Their responsiveness to our input and strange force that causes them to remain overall shape generates a weird fun that cannot be described in words.

Unity, the most popular game engine in the world right now, should provide us with good basis on how to render and handle our Softbodies.
However, this README has an information on how to make it regardless of engine, language you want to use.

## Basics of Meshes

Each mesh has a lot of data in it. In the simplest form, mesh consists of vertices (points in a space) and triangles (defined by those points).

Generating your own mesh isn't a hard task: just give it some points, tell which points generate triangle and *voilà*.

Mesh, that changes it's shape over time, should update it's vertices each frame, so the rendered object fits our data.

For example: 

    1. Create a water surface as a point grid.

    2. Create triangles, so each square of an grid consists of two triangles.

    3. Each point on the grid can be updated each frame with a function: y = sin(x + Time.deltaTime) in a shader or in some code.
       This creates simple 3D water waves.

If it's a vertex shader: job is done.

If we done it in a code (e.g. MonoBehaviour Unity) we should also update our current mesh with: ```mesh.vertices = waveVertices```

There are so many things you can do with vertices, triangles and meshes, but those basics and this idea of changing mesh is crucial in implementing a some sort of Jelly-like object.

## Softbody - Realtime Mesh Deformation

Modifying base vertex that is just ```float x, y, z;``` with velocity, initial position and current deformation position, can give an interesting results.
Adding some pressure/input, modifies all vertices by giving them some velocity based on distance from the "touch point". Touching a balloon makes a small hole and expands whole object in all directions as we reduced volume of an space inside the balloon.

Also, we should reduce velocity of each point each frame, and try to settle the points back onto their original positions.

![](softbody.gif)

This works pretty well with static object that can be touched and their shape doesn't change much.

## Jellybody - Springs and the Mesh


![](jellybody.gif)