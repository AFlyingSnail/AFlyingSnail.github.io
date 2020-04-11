# VTF

### Q1：什么是VTF？

Vertex Texture Fetch顶点纹理拾取，简称VTF，是Shader Model中的特性，本质为在vertex shader中检索纹理。

### Q2：为什么要在vertex shader里检索纹理？

核心理念为：纹理即数组。
通常讲的纹理作为图像，每个像素存储的是颜色值。但现代GPU作为高速并行处理的计算单元，可以做除图像渲染之外的计算。这里纹理可作为大量数据存储的载体，将大量数据（数组）传递给GPU，shader即可访问使用这些数据。

### Q3：VTF存在的意义。

vertex shader通过Fetch纹理传递的数据，进行数据处理。

如：

`// vertex shader`

`vec4 vertexColor = texture2D(sameMap, gl_MultiTexCoord0.xy);`
or
`vec4 vertexColor = texture2DLod(sameMap, gl_MultiTexCoord0.xy,0.0);`

`gl_Position = gl_ProjectionMatrix * (gl_ModelViewMatrix * (gl_Vertex));`


`// pixel shader`

`gl_FragColor = vertexColor;` 

### Q4：VTF的实践

处理地形高度图纹理、混合权重纹理等。

将地形的高度坐标值存储在纹理像素中，VTF取出像素转化为灰度，并转化为地形顶点的“高度”；地形混合权重同理。

### Q5：关于图形库支持

GLES需要shader model和GPU都支持。
GL2.0 shader已支持VTF，在GL2.1中texture float formats并不在core中，需要测试GL_ARB_texture_float.在GL3.0中texture float formats已经集成为core feature。


参考：https://www.khronos.org/opengl/wiki/Vertex_Texture_Fetch

#### 尚未完成..

