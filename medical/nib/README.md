# NIBABEL

## What are the axes in nib?
The axes is based RAS+: </br>
1. Left to Right -> Coronal, sum_axis = 1, sum_out_axes = (0, 2) 
2. Posterior to Anterior -> Sagital, sum_axis = 0, sum_out_axes = (1, 2)
3. Inferior to Superior > Axial, sum_axis = 2, sum_out_axes = (0, 1)

## How to get orientation values?
```python
nib.aff2axcodes(img.affine)
```