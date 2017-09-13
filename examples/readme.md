# threejs 例子代码审阅

## 随意代码

#### 一种初始化Vector3的方法

```js
var positions = new Float32Array( MAX_POINTS * 3 ); // 3 vertices per point
```
来源于：
[next step/how to update things](https://threejs.org/docs/#manual/introduction/How-to-update-things)

#### geometry的 needUpdate 属性

```js
var geometry = new THREE.Geometry();
geometry.verticesNeedUpdate = true;  //顶点数据是否需要更新，如果为false,则更改了顶点，也不会刷新顶点数据（也就是vertices）
geometry.elementsNeedUpdate = true;  //面（face）数据是否需要更新
geometry.morphTargetsNeedUpdate = true;  //未发现
geometry.uvsNeedUpdate = true;  //uv映射数据是否需要更新
geometry.normalsNeedUpdate = true; //法向量数据是否需要更新
geometry.colorsNeedUpdate = true; //颜色数据是否需要更新
geometry.groupsNeedUpdate = true; 
geometry.lineDistancesNeedUpdate = true; //
```