Enable blending first

```cpp
glEnable(GL_BLEND);  
```

## Blending equation

$$
C_{result} = C_{src} * f_{src} + C_{dst} * f_{dst}
$$

- $C_{src}$ : the source color vector. This is the color output of fragment shader
- $C_{dst}$ : the destination color vector. This is the color vector that is currently stored in the color buffer
- $f_{src}$ : the source factor value. Sets the impact of the alpha value on the source color.
- $f_{dst}$ : the destination factor value. Sets the impact of the alpha value on the destination color.


| Option                        | Value                                                                                    |
| ----------------------------- | ---------------------------------------------------------------------------------------- |
| `GL_ZERO`                     | Factor is equal to **0**.                                                                |
| `GL_ONE`                      | Factor is equal to **1**.                                                                |
| `GL_SRC_COLOR`                | Factor is equal to the source color vector $C_{src}$.                                    |
| `GL_ONE_MINUS_SRC_COLOR`      | Factor is equal to **1** minus the source color vector: $1 - C_{src}$                    |
| `GL_DST_COLOR`                | Factor is equal to the destination color vector $C_{dst}$                                |
| `GL_ONE_MINUS_DST_COLOR`      | Factor is equal to **1** minus the destination color vector: $1 -C_{dst}$                |
| `GL_SRC_ALPHA`                | Factor is equal to the ***alpha*** component of the source color vector $C_{src}$        |
| `GL_ONE_MINUS_SRC_ALPHA`      | Factor is equal to ***1−alpha*** of the source color vector $C_{src}$                    |
| `GL_DST_ALPHA`                | Factor is equal to the ***alpha*** component of the destination color vector $C_{dst}$   |
| `GL_ONE_MINUS_DST_ALPHA`      | Factor is equal to ***1−alpha*** of the destination color vector $C_{dst}$               |
| `GL_CONSTANT_COLOR`           | Factor is equal to the constant color vector $C_{constant}$                              |
| `GL_ONE_MINUS_CONSTANT_COLOR` | Factor is equal to ***1*** - the constant color vector $C_{constant}$                    |
| `GL_CONSTANT_ALPHA`           | Factor is equal to the ***alpha*** component of the constant color vector $C_{constant}$ |
| `GL_ONE_MINUS_CONSTANT_ALPHA` | Factor is equal to ***1−alpha*** of the constant color vector $C_{constant}$             |

```cpp
glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);  
```
