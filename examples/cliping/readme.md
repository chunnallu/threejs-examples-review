# 剪切

## 关键代码

局部剪切：

```js
// ***** Clipping planes: *****

				var localPlane = new THREE.Plane( new THREE.Vector3( 0, - 1, 0 ), 0.8 );
				
				
				// Geometry
                
                				var material = new THREE.MeshPhongMaterial( {
                						color: 0x80ee10,
                						shininess: 100,
                						side: THREE.DoubleSide,
                
                						// ***** Clipping setup (material): *****
                						clippingPlanes: [ localPlane ],
                						clipShadows: true
                
                					} );
				
                				renderer.localClippingEnabled = true;
```

全局剪切：

```js
var globalPlane = new THREE.Plane( new THREE.Vector3( - 1, 0, 0 ), 0.1 );
// ***** Clipping setup (renderer): *****
                				var globalPlanes = [ globalPlane ];
                				renderer.clippingPlanes = globalPlanes; // GUI sets it to globalPlanes
```