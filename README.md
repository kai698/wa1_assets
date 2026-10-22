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
