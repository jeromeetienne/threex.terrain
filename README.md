threex.terrain
=============
threex.terrain is a [three.js games extension](http://www.threejsgames.com/extensions/) which provides a procedural terrain generated from a simplex noise, the [Perlin noise](http://en.wikipedia.org/wiki/Perlin_noise). As you can see you have different zones that make the terrain more varied, the blue zone represents water, the green one represents trees or grass and the white zone at the mountain top is snow. Imagine your video game character walking on these 3D mountains or flying over them, pretty cool eh? You can take him through river, forest, wind and snow if you want ;)  

Show Don't Tell
===============
* [examples/canvas.html](http://jeromeetienne.github.io/threex.terrain/examples/canvas.html)
\[[view source](https://github.com/jeromeetienne/threex.terrain/blob/master/examples/canvas.html)\] :
It shows a perlin terrain in a canvas 2d.
* [examples/planegeometry.html](http://jeromeetienne.github.io/threex.terrain/examples/planegeometry.html)
\[[view source](https://github.com/jeromeetienne/threex.terrain/blob/master/examples/planegeometry.html)\] :
It displays the terrain in 3d with three.js.
* [examples/height.html](http://jeromeetienne.github.io/threex.terrain/examples/height.html)
\[[view source](https://github.com/jeromeetienne/threex.terrain/blob/master/examples/height.html)\] :
It show how to test the height in a 3d terrain
* [examples/minecraft.html](http://jeromeetienne.github.io/threex.terrain/examples/minecraft.html)
\[[view source](https://github.com/jeromeetienne/threex.terrain/blob/master/examples/minecraft.html)\] :
It show a minecraft character walking on perlin terrain

A Screenshot
============
[![screenshot](https://raw.githubusercontent.com/jeromeetienne/threex.terrain/master/examples/images/screenshot-threex-terrain-512x512.jpg)](http://jeromeetienne.github.io/threex.terrain/examples/planegeometry.html)

How To Install It
=================

You can install it via script tag

```html
<script src='threex.terrain.js'></script>
```

Or you can install with [bower](http://bower.io/), as you wish.

```bash
bower install threex.terrain
```

How To Use It
=============


To allocate a heightMap with a width of 100 and a depth of 200, do

```javascript
var heightMap	= THREEx.Terrain.allocateHeightMap(100, 200)
```

To generate some heights based on a simplex/perlin noise, do 

```javascript
THREEx.Terrain.simplexHeightMap(heightMap)
```

If you want to display it in three.js, built a ```THREE.PlaneGeometry``` for it

```javascript
// build the geometry
var geometry	= THREEx.Terrain.heightMapToPlaneGeometry(heightMap)
// init the material
var material	= new THREE.MeshPhongMaterial();
// create the mesh and add it to the scene
var mesh	= new THREE.Mesh( geometry, material );
scene.add( mesh );
```

To get the ground height of this mesh, use the following

```javascript
var y = THREEx.Terrain.planeToHeightMapCoords(heightMap, mesh, x, z)
```

It is possible to enhance the rendering of this heightmap with some vertexColor, and a 
smoother shading if you want.

```
// build the geometry
var geometry	= THREEx.Terrain.heightMapToPlaneGeometry(heightMap)
// set the vertexColor in the geometry
THREEx.Terrain.heightMapToVertexColor(heightMap, geometry)
// init the material
var material	= new THREE.MeshPhongMaterial({
	shading		: THREE.SmoothShading,
	vertexColors 	: THREE.VertexColors,
});
// create the mesh and add it to the scene
var mesh	= new THREE.Mesh( geometry, material );
scene.add( mesh );
```

To get the height with heightMap coordinates, just use

```javascript
var y	= THREEx.Terrain.heightMapToHeight(heightMap, x, z)
```

If you want to display the result in a canvas 2d, just do

```javascript
var canvas	= THREEx.Terrain.heightMapToCanvas(heightMap)
document.body.appendChild(canvas)
```

## Possible optimisations
* use shader material to build the perlin in shader
* use THREE.BufferGeometry to boost the generation step


