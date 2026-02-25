
# Unofficial nvdiffrast wheels (CUDA 13.0, Python 3.10, SM_120)

**What is this?** Prebuilt Linux wheels for [NVlabs/nvdiffrast] targeting:
- CUDA **13.0** (`cu130`)
- Python **3.10**
- Torch **2.10**, Torchvision **0.25.0**, Torchaudio **2.10.0**
- GPU archs compiled in: `sm_80; sm_86; sm_89; sm_90; sm_120`  

> Upstream project and docs: [NVlabs/nvdiffrast]. [1](https://github.com/NVlabs/nvdiffrast)

---


## Requirements

- **NVIDIA driver**: R580+ on Linux for CUDA 13.0 (check with `nvidia-smi`). [2](https://docs.nvidia.com/cuda/archive/13.0.0/cuda-toolkit-release-notes/index.html)[3](https://www.servethehome.com/nvidia-cuda-toolkit-13-0-is-out/)  
- **PyTorch**: Install a PyTorch build that matches your CUDA line **before** installing this wheel.

---


## Installation

A) If running exact same targets:
```bash
pip3 install nvdiffrast-0.4.0-cp310-cp310-linux_x86_64.whl
```

B) Otherwise edit the apptainer file (.def) so as to specify different versions, recompile, run (choose 1 or 2) and obtain your custom wheel file:
```bash
apptainer build --sandbox --fakeroot _0nvdiffrast _0nvdiffrast.def

1) apptainer shell -H /home/user/ --pwd / -w --fakeroot _0nvdiffrast
2) apptainer shell -H /home/user/ --pwd / --nv _0nvdiffrast

  cd /nvdiffrast-cu130-wheels && python3 setup.py bdist_wheel
```

If success, wheel will be created at /nvdiffrast-cu130-wheels/dist/.

Renaming it is free to user, but remember pip wheel naming guidelines.

---

## Test

```bash
python3 - <<'PY'
import torch, nvdiffrast.torch as dr
print("Torch:", torch.__version__, "CUDA:", torch.version.cuda)
print("Arch list:", torch.cuda.get_arch_list())
ctx = dr.RasterizeCudaContext(device='cuda:0')
print("nvdiffrast OK:", ctx is not None)
PY
```


See &#x261E;&#x261E; [nvdiffrast documentation](https://nvlabs.github.io/nvdiffrast) &#x261C;&#x261C; for more information.

## Licenses

Copyright &copy; 2020&ndash;2025, NVIDIA Corporation. All rights reserved.

This work is made available under the [Nvidia Source Code License](https://github.com/NVlabs/nvdiffrast/blob/main/LICENSE.txt).

For business inquiries, please visit our website and submit the form: [NVIDIA Research Licensing](https://www.nvidia.com/en-us/research/inquiries/)

Environment map stored as part of `samples/data/envphong.npz` is derived from a Wave Engine
[sample material](https://github.com/WaveEngine/Samples-2.5/tree/master/Materials/EnvironmentMap/Content/Assets/CubeMap.cubemap)
originally shared under 
[MIT License](https://github.com/WaveEngine/Samples-2.5/blob/master/LICENSE.md).
Mesh and texture stored as part of `samples/data/earth.npz` are derived from
[3D Earth Photorealistic 2K](https://www.turbosquid.com/3d-models/3d-realistic-earth-photorealistic-2k-1279125)
model originally made available under
[TurboSquid 3D Model License](https://blog.turbosquid.com/turbosquid-3d-model-license/#3d-model-license).

## Citation

```
@article{Laine2020diffrast,
  title   = {Modular Primitives for High-Performance Differentiable Rendering},
  author  = {Samuli Laine and Janne Hellsten and Tero Karras and Yeongho Seol and Jaakko Lehtinen and Timo Aila},
  journal = {ACM Transactions on Graphics},
  year    = {2020},
  volume  = {39},
  number  = {6}
}
```
