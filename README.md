# Marker based WebAR

## AIM:
To create a Marker-Based WebAR application using MindAR and Three.js, where a 3D model (like glasses) is anchored to a detected facial marker or image marker in real-time through a web browser.

## ALGORITHM:
1.Start the Project Setup
  *Create the project folder with index.html, main.js, and required assets (like 3D models and textures).
  *Add the MindAR library and Three.js to the HTML page.

2.Initialize the AR Engine
  *Use MindARThree from the MindAR library to set up the AR engine, camera, and rendering context.

3.Add Lighting
  *Create a HemisphereLight to properly illuminate the 3D model in the AR scene.

4.Load 3D Model
  *Load a GLTF 3D model (for example, glasses1/scene.gltf) using an async function and a loader helper (loadGLTF()).

5.Create an Anchor
  *Use mindarThree.addAnchor(id) to anchor the 3D model to a specific facial landmark (like nose or eyes).

6.Attach the Model
  *Scale and attach the loaded model to the anchor’s group, so it follows the detected facial feature.

7.Start the AR Session
  *Start the AR engine using mindarThree.start() and continuously render the scene using renderer.setAnimationLoop().

8.View the Output
  *Run the app through a local web server,like NGROK, allow camera access, and observe the 3D object align with the marker or facial region.

## PROGRAM:
***index.html***
```
<html>
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="./libs/mindar/mindar-face-three.prod.js"></script>
    <script src="./main.js" type="module"></script>
    <style>
      html, body {
        position: relative; 
        margin: 0; 
        width: 100%; 
        height: 100%; 
        overflow: hidden;
      }
    </style>
    <link rel="icon" href="data:,">
  </head>
  <body>
  </body>
</html>
```
***main.js***
```
import {loadGLTF, loadTexture} from "./libs/loader.js";
const THREE = window.MINDAR.FACE.THREE;

document.addEventListener('DOMContentLoaded', () => {
  const start = async() => {
    const mindarThree = new window.MINDAR.FACE.MindARThree({
      container: document.body,
    });
    const {renderer, scene, camera} = mindarThree;
  
    const light = new THREE.HemisphereLight( 0xffffff, 0xbbbbff, 1);
    scene.add(light);
    
/* const faceMesh = mindarThree.addFaceMesh();

    const texture = await loadTexture('./asserts/facemesh/face-mask-template/Face_Mask_Template.png');
    faceMesh.material.map = texture;
    faceMesh.material.transparent = true;
    faceMesh.material.needsUpdate = true;
    scene.add(faceMesh); 
*/

const glasses = await loadGLTF('./asserts/models/glasses1/scene.gltf');
glasses.scene.scale.multiplyScalar(0.01);
const anchor = mindarThree.addAnchor(168);
anchor.group.add(glasses.scene);

       await mindarThree.start();
       renderer.setAnimationLoop(() => {
          renderer.render(scene, camera);
       });
     }
     start();
});
```

## OUTPUT:
->When the application runs in the browser with camera access enabled, the AR engine detects the user’s face and attaches the 3D glasses model to the corresponding facial landmark (anchor ID 168).
->As the user moves or tilts their head, the 3D model dynamically follows their face in real time.

## RESULT:
->The Marker-Based WebAR application was successfully implemented using MindAR and Three.js.
->A 3D model was loaded and accurately tracked with a detected face marker, demonstrating the principles of image and face-based AR tracking in the web environment.


