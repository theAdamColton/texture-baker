# Texture baker

Small texture baker which rasterizes barycentric coordinates to a tensor.
It also implements an interpolation module which can be used to bake attributes to textures then.

# Notice

This code originally comes from [stable-fast-3d](https://github.com/Stability-AI/stable-fast-3d/tree/8a1fb7156df24644c850391049c4af7afcdb2ab7/texture_baker)
and is licensed with the STABILITY AI COMMUNITY LICENSE AGREEMENT

I've put this code into a seperate pip-able friendlier format. 

## Installation

First make sure torch is installed 
`pip install torch`

Then you can install this git repo
`pip install git+https://github.com/theAdamColton/texture-baker`

## Usage

The baker can quickly bake vertex attributes to the a texture atlas based on the UV coordinates.
It supports baking on the CPU and GPU.

```python
from texture_baker import TextureBaker

mesh = ...
uv = mesh.uv # num_vertex, 2
triangle_idx = mesh.faces # num_faces, 3
vertices = mesh.vertices # num_vertex, 3

tb  = TextureBaker()
# First get the barycentric coordinates
rast = tb.rasterize(
    uv=uv, face_indices=triangle_idx, bake_resolution=1024
)
# Then interpolate vertex attributes
position_bake = tb.interpolate(attr=vertices, rast=rast, face_indices=triangle_idx)
```
