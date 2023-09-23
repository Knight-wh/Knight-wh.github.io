# Cesium

## Quick

- glTF坐标系统里，长度单位是m，角度单位是弧度。
- 屏幕坐标`movement.position`获取  
- 椭球面坐标`viewer.scene.camera.pickEllipsoid(movemrnt.postion, ellipsoid)`获取

添加调试控件

`viewer.extend(Cesium.viewerCesium3DTilesInspectorMixin);`
`viewer.extend(Cesium.viewerCesiumInspectorMixin);`

## [BIM数据结构](BIM.md)

## Cesium+Threejs解决方案

### 把Three.js当做场景模型加载

非常慢，`Three.js`相当于格式转换工具,`ifcLoader`

### cesium官方博客集成

以`Cesium`创建地球作为地图，`Three.js`场景基于地图上的局部坐标系叠加到`Cesium`场景中，然后在帧渲染前同步两个场景的相机。
参考2017年的博客[intergrating ceisum and threejs](https://cesium.com/blog/2017/10/23/integrating-cesium-with-threejs/)

### 在cesium实现Threejs部分接口

### 从渲染层面实现cesium和threejs的融合

基于Cesium.DrawCommand的Threejs渲染器

***

**解决方案的问题**：把模型当做gltf，没有使用3DTiles。没有学习过threejs，因此不清楚是否可以实现分离式渲染

**参考文章**：[Cesium和Three.js结合的5个方案](https://zhuanlan.zhihu.com/p/441682100)

