# Marker based WebAR

## AIM:


## ALGORITHM:

## PROGRAM:

***index.html***
```
<html>
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="./libs/mindar/mindar-image-three.prod.js"></script>
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

## RESULT:


