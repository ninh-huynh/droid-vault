
## Vertex buffer objects (VBO)

```cpp

float vertices[] = {
    -0.5f, -0.5f,
     0.5f, -0.5f,
     0.0f,  0.5f
};  

unsigned int VBO; 
glGenBuffers(1, &VBO);

```

### Copy vertex data from CPU to GPU

```cpp

glBindBuffer(GL_ARRAY_BUFFER, VBO);
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);

```

>[!tip] Tip
>We can change the `usage` to one of the following value base on what is the most suitable for our use case:
> - `GL_STREAM_DRAW`: the data is set only once and used by the GPU at most a few times
> - `GL_STATIC_DRAW`: the data is set only once and used many times.
> - `GL_DYNAMIC_DRAW`: the data is changed a lot and used many times.

>[!attention] Attention
>The `glBufferData` will do two job: allocate GPU memory and adds data into memory. We could also use the `glBufferSubData` to update the buffer memory only. Example usages: 
>`glBufferSubData(GL_ARRAY_BUFFER, 24, sizeof(data), &data); // Range: [24, 24 + sizeof(data)]
`


Before each draw statement, we have to tell OpenGL how it should interpret the data

![vertex attr](https://learnopengl.com/img/getting-started/vertex_attribute_pointer.png)

```cpp
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);
glEnableVertexAttribArray(0); 
```
## Vertex array objects (VAO)

With VAO, use can save the state of VBO and the vertex state once and the using later by binding it.

![vertex array object](https://learnopengl.com/img/getting-started/vertex_array_objects_ebo.png)

```cpp

// ..:: Initialization code :: ..
// 1. bind Vertex Array Object
glBindVertexArray(VAO);
// 2. copy our vertices array in a vertex buffer for OpenGL to use
glBindBuffer(GL_ARRAY_BUFFER, VBO);
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
// 3. copy our index array in a element buffer for OpenGL to use
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, EBO);
glBufferData(GL_ELEMENT_ARRAY_BUFFER, sizeof(indices), indices, GL_STATIC_DRAW);
// 4. then set the vertex attributes pointers
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);
glEnableVertexAttribArray(0);  

  
// ..:: Drawing code (in render loop) :: ..
glUseProgram(shaderProgram);
glBindVertexArray(VAO);
glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, 0);
glBindVertexArray(0);

```