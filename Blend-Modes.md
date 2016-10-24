***NOTE:*** Not all blend modes work in D3D.

`BLEND_NORMAL`

Normal alpha blending (the default blend mode).

`BLEND_ADD`

Additive blending.

`BLEND_SUBTRACT`

Subtractive blending. Equivalent to `destination = destination - source`

`BLEND_MODULATE`

`BLEND_COPY_SRC`

No blending (replace mode). Equivalent to `destination = source`

`BLEND_ALPHA_MASK`

Alpha mask. Useful for changing alpha at the end of an `ActorFrameTexture` draw.

`BLEND_ALPHA_KNOCK_OUT`

Alpha knockout. Inverse of `BLEND_ALPHA_MASK`. Useful for changing alpha at the end of an `ActorFrameTexture` draw.

`BLEND_ALPHA_MULTIPLY`

Multiply blend based on alpha.

`BLEND_WEIGHTED_MULTIPLY`

Equivalent to `destination = 2*(destination*source)`: `0.5` has no effect, lower darkens, greater lightens the result.

`BLEND_INVERT_DEST`

Inverted blending. Equivalent to `destination = source - destination`

`BLEND_NO_EFFECT`

Does not draw color. Equivalent to `destination = destination`. Useful for depth masking.
