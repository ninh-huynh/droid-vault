As mentioned in the [[Coordinate System]], the default uniform coordinate system of OpenGL could cause the shape being drawn skewed. So it must have have some way to deal with this. The solution is using the combination of multiple transformation matrix; including model matrix, view matrix, projection matrix.

## Model matrix
This matrix will transform our coordinate from local space to world space. The transformation it perform including translates, scales and rotates.

```kotlin
import android.opengl.Matrix

// ...

val modelMatrix = FloatArray(16)
Matrix.setIdentityM(modelMatrix, 0)
            
Matrix.translateM(modelMatrix, 0, rectX, rectY, 0f)
Matrix.rotateM(modelMatrix, 0, angle, 0f, 0f, 1f)
Matrix.scaleM(modelMatrix, 0, scaleX, scaleY, 1f)

```

> [!attention] Attention
> There are a lot of different way to compute the model matrix. And each way require a correct position coordinate of the object to be draw. When working with object have fixed size in pixel based coordinate, we could use the pixel based coordinate for our life easier. Also, to be able to use the `modelMatrix` described above, we have to make sure our object have size 1x1 and the original is at the center.


## View matrix
Since we working with only 2D object, this step could ignore to simplify the transformation.

## Projection matrix

The below code will create a clipping space have the origin (0, 0) at the **bottom left**.

```kotlin
import android.opengl.Matrix

// ...

val projectionMatrix = FloatArray(16)
Matrix.setIdentityM(projectionMatrix, 0)

Matrix.orthoM(projectionMatrix, 0, 0f, width, 0f, height, -1f, 1f)

```

>[!hint] Hint
>We could also define a clipping space have the origin (0,0) at the **top left** by swapping the `top`, `bottom` parameter.

## Final matrix

After we have compute the model matrix and the projection matrix, let combine them into a single transformation by multiple it.

```kotlin

import android.opengl.Matrix

val mvpMatrix = FloatArray(16)
Matrix.setIdentityM(mvpMatrix, 0)

Matrix.multiplyMM(mvpMatrix, 0, projectionMatrix, 0, modelMatrix, 0)

```

