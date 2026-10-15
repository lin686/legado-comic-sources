# Legado 漫画书源合集（102 条）

本仓库收录 **102 条 Legado（阅读 App）漫画书源**，全部启用，可用于阅读 App 的「网络导入 / 订阅」。

> 原始来源文件名为 `100+官方图源合集.json`，实际内容为漫画书源（`bookSourceType: 漫画`）。

## 文件说明

| 文件 | 格式 | 用途 |
| --- | --- | --- |
| `legado-comic-sources.json` | 标准 JSON 数组（UTF-8，未压缩） | **推荐**。阅读 App 网络导入 / 订阅直接使用 |
| `legado-comic-sources.compressed.json` | 原始格式（zlib 压缩后 Base64） | 保留原始数据包，供支持该格式的分享站/工具使用 |

## 拉取下载（Raw 链接）

标准 JSON：

```
https://raw.githubusercontent.com/lin686/legado-comic-sources/main/legado-comic-sources.json
```

原始压缩包：

```
https://raw.githubusercontent.com/lin686/legado-comic-sources/main/legado-comic-sources.compressed.json
```

## 在阅读 App 中导入

1. 打开「阅读」App → 底部「我的」。
2. 进入「书源管理」。
3. 右上角菜单 →「网络导入」。
4. 粘贴上面的 **标准 JSON Raw 链接**，确认导入即可。

## 命令行拉取

```bash
# 拉取标准 JSON
curl -L -o legado-comic-sources.json \
  https://raw.githubusercontent.com/lin686/legado-comic-sources/main/legado-comic-sources.json

# 拉取原始压缩包
curl -L -o legado-comic-sources.compressed.json \
  https://raw.githubusercontent.com/lin686/legado-comic-sources/main/legado-comic-sources.compressed.json
```

## 说明与免责

- 书源规则来自公开渠道，仅供个人学习与技术研究使用。
- 各书源的可用性取决于其目标站点的实际状态，可能随时失效，本仓库不对可用性作保证。
- 请勿将本仓库内容用于任何商业用途。
