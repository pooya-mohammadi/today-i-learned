# Torch
## How to load model.safetensors
```
from safetensors.torch import safe_open
with safe_open("model.safetensors", framework="pt", device="cpu" as f:
    for key in f.keys():
        print(key, f.get_tensor(key).shape)
```
