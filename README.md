# pytorch-win_amd64-cpu-wheels

`win_amd64` wheels reuploaded from https://download.pytorch.org/whl/torch_stable.html. This is done mainly to avoid `poetry` errors when adding `torch` dependency: constructs like

```toml
[tool.poetry.dependencies]
torch = [
    { version = "^1.6.0", platform = "linux" },
    { version = "^1.6.0", platform = "darwin" },
    { url = "https://download.pytorch.org/whl/cpu/torch-1.6.0%2Bcpu-cp36-cp36m-win_amd64.whl", platform = "windows", python = "~3.6" },
    { url = "https://download.pytorch.org/whl/cpu/torch-1.6.0%2Bcpu-cp37-cp37m-win_amd64.whl", platform = "windows", python = "~3.7" },
    { url = "https://download.pytorch.org/whl/cpu/torch-1.6.0%2Bcpu-cp38-cp38-win_amd64.whl", platform = "windows", python = "~3.8" },
]
```

result in obscure internal errors when running `poetry update`, and I'm too tired to write the `poetry.lock` by myself.

### Get an installable `torch` (CPU version) on all three platforms:

`pyproject.toml`

```toml
[tool.poetry.dependencies]
torch = "^1.6.0"

[[tool.poetry.source]]
name = "hoefling-pypi-private"
url = "https://hoefling.io/pypi"
secondary = true
```

`poetry.lock`

```toml
torch = [
    ...,
    {file = "torch-1.6.0-cp36-cp36m-win_amd64.whl", hash = "sha256:bb5bdd1bf068ca8d459bd79ab08c22f2442d2aef616695d8857cbe5c25c9cba9"},
    {file = "torch-1.6.0-cp37-cp37m-win_amd64.whl", hash = "sha256:0c29e4df4527a54d43cc0f3cf6369239bc39a898ad21350502387f27653f3553"},
    {file = "torch-1.6.0-cp38-cp38-win_amd64.whl", hash = "sha256:c48b9fa604802d1dd1cf04e78f3abe04ea402ff70cfcd5f8032e3fde6ffbfb01"},
]
```
