## 使用缓冲区对象向顶点着色器传入顶点数据的步骤

### WebGL1

- 创建缓冲区对象
- 绑定缓冲区对象
- 将数据写入缓冲区对象
- 告诉`attribute`变量如何从缓冲区读取数据。将缓冲区对象分配给一个`attribute`变量
- 开启`attribute`变量。连接变量与分配给它的缓冲区对象

### WebGL2

- 创建缓冲区对象
- 绑定缓冲区对象
- 将数据写入缓冲区对象
- **创建顶点数组对象。vertex array object(attribute state)**
- **绑定顶点数组对象**
- 开启`attribute`变量
- 告诉`attribute`变量如何从缓冲区读取数据。将缓冲区对象分配给一个`attribute`变量

---

**初始化阶段**

- 创建所有着色器和程序并寻找参数位置
- 创建缓冲并上传顶点数据
- 为您要绘制的每个事物创建一个顶点数组
  - 为每个属性调用 gl.bindBuffer, gl.vertexAttribPointer, gl.enableVertexAttribArray
  - 绑定索引到 gl.ELEMENT_ARRAY_BUFFER
- 创建纹理并上传纹理数据

**渲染阶段**

- 清空并设置视图和其他全局状态（开启深度检测，剔除等等）
- 对于想要绘制的每个物体
  - 调用 gl.useProgram 使用需要的程序
  - 为物体绑定顶点数组
    - 调用 gl.bindVertexArray
  - 设置物体的全局变量
    - 为每个全局变量调用 gl.uniformXXX
    - 调用 gl.activeTexture 和 gl.bindTexture 设置纹理到纹理单元
  - 调用 gl.drawArrays 或 gl.drawElements

#### 代码解释

`gl.bindBuffer(target, buffer)`中`target`表示缓冲区对象的用途，或者是绑定点。

`gl.bufferData(target, data, usage)`开辟存储空间，向绑定在`target`上的缓冲区对象中写入数据`data`。

## `gl.useProgram()`

`gl.useProgram()`放置的位置可以随意，与上面创建缓冲区传数据中的所有操作“无关”

## some qusetions

在webgl2的示例代码中，`gl.unifrom2v()`要放在`gl.usePromgram()`的后面，才能绘制正确的图形。

## 纹理坐标

纹理映射过程，首先在顶点着色器中为每个顶点指定纹理坐标，然后在片元着色器中根据每个片元的纹理坐标从纹理图像中抽取纹素颜色。

WebGL通过纹理单元的机制来同时使用多个纹理。每个纹理单元有一个单元编号来管理一张纹理图形。系统支持的纹理单元的个数取决于硬件和浏览器的WebGL实现。例如`gl.TEXTRUE0`

# WebGL渲染与投影矩阵

在《WebGL编程指南》第七章正射投影一节中，在旋转三角形到某个角度时，三角形的一个角开始消失，书中指出是“没有指定可视范围，WebGL只显示可视范围内的区域。P233页”。对此的详细解释是，从所周知，通过投影矩阵，我们会把可视空间压缩成一个三维均在[-1,1]的立方体空间中，WebGL会绘制渲染该立方体里全部场景。而书中案例在旋转三角形时，消失的部分的z值可能超过了-1.0，因此没有被绘制出来。同样也可以解释为什么从视点到近平面的物体可以不被渲染，而根据直觉，这些物体应该被“看见”。
