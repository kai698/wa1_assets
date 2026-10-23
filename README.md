# wa1_assets

WA1 机器人模型资产仓库。模型文件由 Git LFS 管理。

## 拉取模型

首次使用前安装并初始化 Git LFS：

```bash
sudo apt update
sudo apt install git-lfs
git lfs install
```

克隆仓库并下载实际网格文件：

```bash
git clone https://github.com/kai698/wa1_assets.git
cd wa1_assets
git lfs pull
```

验证 LFS 文件：

```bash
git lfs ls-files
git check-attr filter -- WA1_400L/meshes/BASE.STL
```

`git lfs ls-files` 应列出 `WA1_400L/meshes/` 下的模型，属性检查应返回 `filter: lfs`。
如果模型文件仍以 `version https://git-lfs.github.com/spec/v1` 开头，说明 LFS 对象尚未下载成功。

## 生成配置和 MJCF

项目环境统一由 `uv` 管理，使用 Python 3.11、PyYAML 和 MuJoCo。首次创建并激活环境：

```bash
uv venv --python 3.11 .venv
source .venv/bin/activate
uv pip install PyYAML mujoco
```

激活后使用 `uv` 运行转换入口：

```bash
uv run --active main.py WA1_400L --override
uv run --active main.py WA1_400L --convert
```

第一条命令从 `WA1_400L.urdf` 生成 `WA1_400L/robot_cfg.yaml`；已有配置默认会被复用，只有传入 `--override` 才会重新生成。第二条命令生成 `WA1_400L/WA1_400L.xml` 和配套的 `scene.xml`，生成的 MJCF 可直接由 MuJoCo 加载。
