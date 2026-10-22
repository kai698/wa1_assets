# wa1_assets

WA1 机器人模型资产仓库。当前资产为 WA1_400L，包含 URDF 和 meshes/ 下的 STL 网格。

## Git LFS

网格、纹理和其他二进制资产由 Git LFS 管理。仓库中的 LFS 指针只保存对象哈希和实际文件大小，模型内容存储在 LFS 服务端。

首次使用前安装并初始化 Git LFS：

```bash
sudo apt update
sudo apt install git-lfs
git lfs install
```

克隆后下载实际网格文件：

```bash
git clone https://github.com/kai698/wa1_assets.git
cd wa1_assets
git lfs pull
```

如果文件仍以 version https://git-lfs.github.com/spec/v1 开头，说明当前文件是指针，尚未成功下载 LFS 对象。

检查 LFS 状态：

```bash
git lfs ls-files
git check-attr filter -- WA1_400L/meshes/BASE.STL
```

git lfs ls-files 应列出 WA1_400L/meshes/ 下的模型，属性检查应返回 filter: lfs。

## 提交新资产

确保已执行 git lfs install，然后像普通 Git 文件一样提交：

```bash
git add WA1_400L/meshes/NEW_PART.STL
git commit -m "add WA1 mesh"
git push
```

匹配 .gitattributes 的文件会自动上传到 Git LFS。不要手动把 LFS 指针内容写入模型文件。

## 历史迁移说明

现有 STL 历史已迁移到 Git LFS。迁移会改变提交哈希；首次推送迁移后的 main 需要维护者确认并使用：

```bash
git push --force-with-lease origin main
```

推送前请先通知其他协作者重新克隆或基于新的 main 重置本地分支。

## 目录约定

```text
WA1_400L/
├── WA1_400L.urdf
└── meshes/
    └── *.STL
```

URDF 中的网格路径相对于机器人目录解析，例如 meshes/BASE.STL。
