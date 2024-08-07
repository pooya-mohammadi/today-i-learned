# NIBABEL

## What are the axes in nib?
The axes is based RAS+: </br>
1. Left to Right -> Coronal 
2. Posterior to Anterior -> Sagital
3. Inferior to Superior > Axial

## How to get orientation values?
```python
nib.aff2axcodes(img.affine)
```