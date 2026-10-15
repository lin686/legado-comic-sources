# 异次元漫画 · 图源合集

本仓库收录多份**异次元漫画 App 的图源**，全部启用。

## ⚠️ 格式说明（重要，务必先读）

本仓库文件是 **「异次元漫画」图源格式**，**不是 Legado（阅读 App）书源格式**，两者不通用。

判别依据（字段名差异）：

| 项目 | 异次元图源（本仓库） | Legado 书源 |
| --- | --- | --- |
| 搜索字段 | `ruleSearchUrl` / `ruleSearchList` / `ruleSearchNoteUrl` | `searchUrl` / `ruleSearch.bookList` / `ruleSearch.bookUrl` |
| 目录字段 | `ruleChapterList` | `ruleToc.chapterList` |
| 内容字段 | `ruleBookContent` | `ruleContent.content` |
| 类型字段 | `bookSourceType: "漫画"`（字符串） | `bookSourceType: 2`（整数） |
| 启用字段 | `enable` | `enabled` |
| 发现字段 | `ruleFindUrl` | `exploreUrl` |

**若要在「阅读」(Legado) 中使用，需要先做格式转换**（见文末「格式转换」）。直接导入会失败或规则错乱。

> 原始来源已确认：本仓库 `legado-comic-sources.json` 与 `yiciyuan123/yiciyuan` 仓库的 `bayuezuixintuyuan.json` **SHA1 完全一致**（`b1f8e72e497060ba02262ab82562e0f70c9eb062`），即「102+ 图源合集」。文件采用 **zlib 压缩 + Base64** 编码。

## 文件说明

### 一、原始合集（102 条）

| 文件 | 格式 | 用途 |
| --- | --- | --- |
| `legado-comic-sources.json` | 标准 JSON 数组（UTF-8，未压缩） | **推荐**，阅读 App 网络导入 / 订阅直接使用 |
| `legado-comic-sources.compressed.json` | 原始格式（zlib 压缩后 Base64） | 保留原始数据包 |

### 二、合并增强版（104 条）

由 `entr0pia/MyLegadoSource`（54 条）+ `kettly1260/ycy-cimoc`（52 条）合并去重而成，并修复了上游数据缺陷（见下方「数据修复说明」）。

| 文件 | 格式 | 用途 |
| --- | --- | --- |
| `legado-comic-sources-merged.json` | 标准 JSON 数组（UTF-8，未压缩） | **推荐**，阅读 App 网络导入 / 订阅直接使用 |
| `legado-comic-sources-merged.compressed.json` | 标准格式的 zlib+Base64 压缩版 | 与原文件编码保持一致，便于工具处理 |

**合并过程**：106 条 → 去重 2 条 → **104 条**，全部 `bookSourceType: 漫画`、全部 `enable: true`。

**数据修复说明**（针对上游 `kettly1260/ycy-cimoc` 的 52 条）：

1. `enable` 原为 **全部 false** → 已统一置为 `true`（否则导入后不会生效）。
2. **缺少 `bookSourceType` 字段** → 已补为 `漫画`（否则阅读 App 会默认当作小说，漫画分类下不显示）。
3. `bookSourceGroup` 绝大多数为空 → 已补为 `异次元`，便于与另一来源区分。

## 拉取下载（Raw 链接）

合并增强版（104 条）：

```
https://raw.githubusercontent.com/lin686/legado-comic-sources/main/legado-comic-sources-merged.json
```

合并增强版压缩包：

```
https://raw.githubusercontent.com/lin686/legado-comic-sources/main/legado-comic-sources-merged.compressed.json
```

原始合集（102 条）：

```
https://raw.githubusercontent.com/lin686/legado-comic-sources/main/legado-comic-sources.json
```

原始压缩包：

```
https://raw.githubusercontent.com/lin686/legado-comic-sources/main/legado-comic-sources.compressed.json
```

## 在「异次元漫画」中导入

1. 打开异次元漫画 → 书架页左上角菜单（≡）。
2. 进入「图源」。
3. 右上角「⋮」→「网络导入」（也可用「本地导入」选文件）。
4. 粘贴上面的 **明文 JSON 链接**，确认后等待加载完成。

> 若 `raw.githubusercontent.com` 在你的网络下不可达，可改用 GitHub API 通道：
> `gh api repos/lin686/legado-comic-sources/contents/legado-comic-sources-merged.json -H "Accept: application/vnd.github.raw+json"`

### 国内加速链接（免代理，2026-10-15 无代理直连实测）

`raw.githubusercontent.com` 在国内被 DNS 污染 / 连接重置，导致「网络导入」失败（实测直连报 `WinError 10054 远程主机强迫关闭了一个现有的连接`）。**改用下面的加速通道即可免代理直连**（已在禁用代理的情况下逐条验证，均成功返回完整 104 条）：

| 通道 | 链接 | 实测耗时 |
| --- | --- | --- |
| jsDelivr (Fastly) | `https://fastly.jsdelivr.net/gh/lin686/legado-comic-sources@main/<文件名>` | 1.3s |
| ghfast.top | `https://ghfast.top/` + 原始 raw 链接 | 1.6s |
| jsDelivr (Cloudflare) | `https://cdn.jsdelivr.net/gh/lin686/legado-comic-sources@main/<文件名>` | 2.6s |
| gh-proxy.com | `https://gh-proxy.com/` + 原始 raw 链接 | 2.9s |
| ghproxy.net | `https://ghproxy.net/` + 原始 raw 链接 | 3.0s |
| jsDelivr (CF 备用) | `https://testingcf.jsdelivr.net/gh/lin686/legado-comic-sources@main/<文件名>` | 3.9s |
| jsDelivr (Gcore) | `https://gcore.jsdelivr.net/gh/lin686/legado-comic-sources@main/<文件名>` | 5.7s |

直接可用示例（合并增强版 104 条，复制任意一条粘贴到「网络导入」）：

```
https://ghfast.top/https://raw.githubusercontent.com/lin686/legado-comic-sources/main/legado-comic-sources-merged.json
```

```
https://cdn.jsdelivr.net/gh/lin686/legado-comic-sources@main/legado-comic-sources-merged.json
```

> 注意：**网络导入请只用明文 JSON**。`.compressed.json` 的 zlib+Base64 格式是部分分享站自有格式，图源 App 原生不认。
>
> 若所有加速通道仍不可用，可把 JSON 下载到手机后用「图源 → 右上角 → 本地导入」。

## 命令行拉取

```bash
# 合并增强版（104 条）
curl -L -o legado-comic-sources-merged.json \
  https://raw.githubusercontent.com/lin686/legado-comic-sources/main/legado-comic-sources-merged.json

# 原始合集（102 条）
curl -L -o legado-comic-sources.json \
  https://raw.githubusercontent.com/lin686/legado-comic-sources/main/legado-comic-sources.json
```

## 数据来源

| 来源仓库 | 条目数 | 说明 |
| --- | --- | --- |
| `yiciyuan123/yiciyuan` → `bayuezuixintuyuan.json` | 102 | 即本仓库原始文件，**SHA1 完全一致**已核验；该仓库另有 17 份图源文件，单份最多 180 条 |
| `entr0pia/MyLegadoSource` → `comicSource.txt` | 53（去内部重复后） | 异次元格式，字段完整，分组标注清晰 |
| `kettly1260/ycy-cimoc` → `comic-source.txt` | 52 | 异次元格式，`enable` 全为 false 且缺 `bookSourceType`，已修复 |

## 更多图源来源（同生态）

`yiciyuan123/yiciyuan` 仓库持续更新，含多份图源合集（走 jsDelivr 国内直连）：

| 文件 | 条数 |
| --- | --- |
| `sanyuetuyuan.json` / `siyuetuyuan.json` | 180 |
| `zuixinhejituyuan.json` | 169 |
| `eryuetuyuan.json` | 149 |
| `ershisantuyuan.json` | 109 |
| `sanyuezuixintuyuan.json` | 104 |
| `bayuezuixintuyuan.json` | 102 |

```
https://gcore.jsdelivr.net/gh/yiciyuan123/yiciyuan/sanyuetuyuan.json
```

## 格式转换（异次元 ↔ Legado）

两者格式不通用，如需互转，可使用开源工具 **`Tthfyth/source`**（支持 Legado 书源 ↔ 异次元图源双向转换，含可视化编辑与规则调试）。

字段对应关系：

| Legado | 异次元 |
| --- | --- |
| `searchUrl` | `ruleSearchUrl` |
| `ruleSearch.bookList` | `ruleSearchList` |
| `ruleSearch.name` | `ruleSearchName` |
| `ruleSearch.bookUrl` | `ruleSearchNoteUrl` |
| `ruleBookInfo.name` | `ruleBookInfoName` |
| `ruleToc.chapterList` | `ruleChapterList` |
| `ruleContent.content` | `ruleBookContent` |

> ⚠️ 部分异次元图源的正文/目录规则是**加密串**（形如 `:_H001_xxxx==`），转换前需先解密，否则转换结果不可用。

## 说明与免责

- 图源规则来自公开渠道，仅供个人学习与技术研究使用。
- 各图源的可用性取决于其目标站点的实际状态，可能随时失效，本仓库不对可用性作保证。
- 请勿将本仓库内容用于任何商业用途。
