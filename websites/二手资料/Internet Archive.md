# Internet Archive

<!--
  本文件分两部分：
  - 分割线以上：用户文档，面向普通用户，语言简洁易懂，不含技术细节
  - 分割线以下：开发者文档，面向程序员，包含 API、HTML 解析、下载逻辑等技术细节
-->

互联网档案馆（Internet Archive）是全球最大的非营利性数字图书馆，致力于“普及所有知识”（Universal Access to All Knowledge）。它不仅收录了数千亿网页快照（Wayback Machine），还拥有数千万册图书、音视频等多媒体档案，是获取海外古籍数字化资源的重要来源。

- 网站链接：https://archive.org/
- 分享协议：[公有领域](https://creativecommons.org/publicdomain/mark/1.0/) / [各资源各异](https://archive.org/about/terms.php)
- 规模：5600万+ 册图书和文本
- 资源类型：古籍扫描件、现代图书、网页快照、音视频
- 支持 IIIF 协议（官方支持），支持 [bookget](https://github.com/deweizhu/bookget) 下载

## 搜索与浏览

- 搜索页面：https://archive.org/advancedsearch.php
- **普通搜索**：主页搜索框直接输入书名、作者或 ISBN。
- **高级搜索**：建议使用高级搜索页，可精确限定 `Title`（书名）、`Creator`（作者）、`Date`（年份）等字段，支持布尔逻辑（AND/OR/NOT）。
- **筛选**：搜索结果页左侧提供丰富的筛选器，如 Media Type（媒体类型，选 Texts）、Year（年份）、Language（语言）、Collection（收藏机构）。
- **借阅与下载**：
  - **公有领域古籍**：通常可直接免费下载 PDF、DjVu 或纯文本。
  - **受版权保护图书**：需要注册账号并“借阅”（Borrow），类似实体图书馆，到期自动归还。

## 每本书能看到什么

以一本古籍详情页为例：

| 字段 | 说明 | 示例 |
|------|------|------|
| Title | 书名 | The Adventures Of Tom Sawyer |
| Author | 作者 | Twain, Mark, 1835-1910 |
| Publication date | 出版年份 | 1876 |
| Publisher | 出版社 | American Publishing Company |
| Collection | 所属集合 | library_of_congress; americana |
| Identifier | 唯一标识符| adventuresoftoms00twai |
| Rights | 版权声明 | Public Domain |

**特色功能**：
- **BookReader**：优秀的在线阅读器，支持单/双页切换、缩放、朗读。
- **全文搜索**：支持在书内搜索关键词（Search inside）。
- **多种格式**：提供 PDF, ePub, DjVu, Kindle (MOBI), Plain Text, DAISY 等多种格式下载。

## 示例

- 详情页：[The Adventures Of Tom Sawyer](https://archive.org/details/adventuresoftoms00twai)
- 在线阅读：[BookReader 视图](https://archive.org/details/adventuresoftoms00twai/page/n7/mode/2up)
- 文件下载列表：[Download Files](https://archive.org/download/adventuresoftoms00twai)

---

# 开发者文档

## URL 结构

### 1. 详情页 (Details Page)
```
https://archive.org/details/{Identifier}
```
- `{Identifier}`: 资源的唯一 ID，如 `adventuresoftoms00twai`。
- **用途**：用户访问的主入口，展示元数据和在线阅读器。

### 2. 下载目录 (Download Directory)
```
https://archive.org/download/{Identifier}
```
- **用途**：列出该资源下的所有原始文件和衍生文件（OCR、缩略图等），支持直接下载。

### 3. 具体文件下载
```
https://archive.org/download/{Identifier}/{Filename}
```
- `{Filename}`: 具体文件名，如 `adventuresoftoms00twai.pdf`。

## 搜索 API

Internet Archive 提供强大的 **Advanced Search API (q)**。

- **URL**: `https://archive.org/advancedsearch.php`
- **Method**: `GET`
- **Parameters**:
  - `q`: 查询字符串，支持 Lucene 语法。例如 `title:"Tom Sawyer" AND mediatype:texts`。
  - `fl[]`: 返回字段列表（fields），如 `identifier,title,creator,date`。
  - `rows`: 返回行数，默认 50。
  - `output`: 输出格式，推荐 `json`。
  - `sort[]`: 排序，如 `date desc`。

**示例**: 搜索 "Chinese classics"
```
https://archive.org/advancedsearch.php?q=Chinese+classics+AND+mediatype:texts&fl[]=identifier&fl[]=title&fl[]=year&rows=5&output=json
```

## 元数据获取

### Metadata API (MDAPI)
获取单个资源的完整元数据（包含所有文件列表）。

- **URL**: `https://archive.org/metadata/{Identifier}`
- **Method**: `GET`
- **Response**: JSON 格式，包含 `metadata` (描述信息), `files` (文件列表), `reviews` 等。

**字段映射**:

| 中文字段 | JSON 路径 (metadata.*) |
|---------|---------|
| 题名 | `metadata.title` |
| 著者 | `metadata.creator` |
| 年代 | `metadata.date` 或 `metadata.year` |
| 出版社 | `metadata.publisher` |
| 来源/收藏 | `metadata.collection` (数组) |
| 语言 | `metadata.language` |
| 描述 | `metadata.description` (HTML) |

## 下载

### 1. 直接下载 (Direct Download)
遍历 Metadata API 返回的 `files` 数组，找到所需格式的文件（如 `format: "DjVu"`, `format: "Text PDF"`）。
- **构造 URL**: `https://archive.org/download/{Identifier}/{file.name}`
- **注意**: 若 `archive.org` 不可用，可使用 `workable_servers` 字段中的镜像地址。

### 2. IIIF 支持
Internet Archive 官方支持 IIIF Presentation API 3.0 和 Image API。
- **Manifest URL**: `https://iiif.archive.org/iiif/3/{Identifier}/manifest.json`
- **Image API Base**: `https://iiif.archive.org/iiif/3/{Identifier}/{Filename}` (注意：需要具体到图像文件名，通常用于 JP2 原图)

### 3. bookget
bookget 原生支持 Internet Archive 下载。
- **原理**: 解析 `metadata` 接口，并发下载 `files` 中的目标文件。

### 4. 批量下载
建议使用官方命令行工具 `ia` (internetarchive python CLI) 或 `wget` 配合文件列表。
- `ia download {Identifier}`
