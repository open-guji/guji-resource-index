# FamilySearch - 中國族譜收藏 1239-2014年

<!--
  本文件分两部分：
  - 分割线以上：用户文档，面向普通用户，语言简洁易懂，不含技术细节
  - 分割线以下：开发者文档，面向程序员，包含 API、HTML 解析、下载逻辑等技术细节
-->

FamilySearch（家谱搜索）是耶稣基督后期圣徒教会运营的全球最大家谱网站。"中國族譜收藏 1239-2014年"（China Collection of Genealogies）是其核心中文族谱合集，汇集了来自中国、北美及东南亚各机构和私人收藏的家谱文献，自 1978 年起与上海图书馆、中国国家图书馆等机构合作采集，是目前全球最大的在线中文族谱数据库。

- 网站链接：https://www.familysearch.org/en/search/collection/1787988
- 分享协议：免费访问，需注册账号；部分图像仅限 FamilySearch 家族史中心（Family History Center）现场查看
- 约 65,000+ 部家谱（jiapu），超过 1,300 万张图像（截至 2020 年 1 月）
- 资源类型：族谱（家谱/jiapu）、宗族谱系、世系图、传记、民事记录
- 时间跨度：1239-2014 年，集中于清代及民国时期（约 1700 年代至 1900 年代初）
- 语言：中文（部分含满文）
- 不支持 IIIF 协议
- bookget 支持下载（仅限缩微胶片图像，2025 年 2 月 13 日后仅支持单一 URL 格式）

## 搜索与浏览

**需要注册免费账号并登录后才能查看图像。**

### 族谱专用搜索（推荐）

FamilySearch 为中文族谱提供了专用搜索界面：

1. 登录 https://www.familysearch.org
2. 点击顶部导航的"搜索"（Search） > "图像"（Images）
3. 在"地点"（Place）字段输入"China"
4. 系统会提示是否使用中文家谱搜索，选择"是"
5. 可按**姓氏**（支持拼音和汉字）和**地点**（省、县）浏览
6. 高级搜索支持按**祠堂名**、**关键词**、**字辈诗**等筛选

### 集合浏览页

- 浏览入口：https://www.familysearch.org/search/image/index?owc=https://www.familysearch.org/recapi/sord/collection/1787988/waypoints
- 按姓氏（Family Name）组织，逐级选择：**姓氏 → 国家（中国） → 省 → 县 → 具体家谱**

### 注意事项

- 本合集为**纯图像浏览**（browse-only），个人姓名**未建索引**，无法按人名搜索
- 需要手动翻阅图像查找特定祖先
- FamilySearch 近期因隐私法规审查暂停了部分中文家谱的访问权限，部分图像可能暂时不可用

## 每本书能看到什么

由于本合集为纯图像浏览，元数据信息相对有限：

| 字段 | 说明 | 示例 |
|------|------|------|
| 姓氏 | 家谱所属姓氏 | 顏 |
| 书名 | 族谱名称 | 顏氏宗譜[8卷首1卷] |
| 地点 | 省/县 | 湖南省 長沙 |
| 胶片号 | 缩微胶片编号（GS Film Number） | 1611089 |
| DGS 号 | 数字化图像组编号 | 004578296 |
| 图像数 | 该册图像总页数 | 87 张 |

- 可在线逐页翻阅扫描图像
- 无 PDF 下载功能
- 无全文文字（OCR）
- 图像来源于缩微胶片数字化，质量因原始胶片状况而异

## 示例

- 合集首页：https://www.familysearch.org/en/search/collection/1787988
- 浏览页面：https://www.familysearch.org/search/image/index?owc=https://www.familysearch.org/recapi/sord/collection/1787988/waypoints
- 目录记录示例（顏氏宗譜）：https://www.familysearch.org/search/catalog/1976741
- 单张图像示例：https://www.familysearch.org/ark:/61903/3:1:3QSQ-G9DL-LLT2

---

# 开发者文档

## URL 结构

### 合集首页
```
https://www.familysearch.org/en/search/collection/1787988
```
- `1787988`：合集 ID（Collection ID）

### Waypoints 浏览页（图像索引）
```
https://www.familysearch.org/search/image/index?owc=https://www.familysearch.org/recapi/sord/collection/1787988/waypoints
```

### 目录记录页
```
https://www.familysearch.org/search/catalog/{catalog_id}
```
- `catalog_id`：FamilySearch 目录记录 ID

### 单张图像（ARK 标识符）
```
https://www.familysearch.org/ark:/61903/3:1:{image_id}
```
- `61903`：FamilySearch 的 ARK NAAN（Name Assigning Authority Number）
- `3:1:{image_id}`：图像的唯一标识，如 `3QSQ-G9DL-LLT2`
- 查询参数（`?lang=zh-Hant&i=0` 等）不影响图像获取

## 搜索 API

### Waypoints API

FamilySearch 使用 waypoints 机制组织浏览导航：

```
GET https://www.familysearch.org/service/cds/recapi/sord/collection/1787988/waypoints
```

返回合集的顶层导航节点（按姓氏分组）。逐级展开获取下级节点。

### 目录搜索

```
GET https://www.familysearch.org/search/catalog/results?count=20&query=%2Bkeywords%3A{关键词}
```

可按胶片号搜索：
```
GET https://www.familysearch.org/search/catalog/results?count=20&query=%2Bfilm_number%3A{胶片号}
```

### 图像数据 API

```
POST https://www.familysearch.org/search/filmdatainfo/image-data
```

需要认证，用于获取特定胶片/图像组的 DeepZoom 信息。

## 元数据获取

本合集为纯图像浏览型，元数据主要从两个来源获取：

### 1. Waypoints 导航树
通过逐级请求 waypoints API 获取姓氏、地区层级结构。

### 2. 目录 API
通过 catalog ID 获取书目信息，但无公开的结构化 JSON API 文档。页面为服务端渲染，元数据需从 HTML 解析。

### 字段映射

| 中文字段 | 提取方式 |
|---------|---------|
| 书名 | HTML 页面标题 / catalog 页 `<h1>` |
| 姓氏 | Waypoint 导航层级 |
| 省/县 | Waypoint 导航层级 |
| 胶片号 | Catalog 页面中 Film/DGS Number 字段 |
| DGS号 | Catalog 页面中 Digital Note 字段 |

## 下载

### bookget 支持

bookget 通过 `app/familysearch.go` 支持 FamilySearch 下载。

**支持的 URL 格式（2025 年 2 月 13 日后仅此一种）：**
```
https://www.familysearch.org/ark:/61903/3:1:{image_id}
```

**关键技术细节：**

1. **认证方式**：需要 FamilySearch 账号的 `fssessionid` Cookie
   - 从 cookie 文件中提取 `fssessionid`
   - 转换为 Bearer Token：`Authorization: bearer {fssessionid}`

2. **必需的 HTTP 请求头**：
   - `Authorization: bearer {fssessionid}`
   - `Cookie: {完整 cookie 字符串}`
   - `Origin: https://www.familysearch.org`
   - `Referer: https://www.familysearch.org/`
   - `User-Agent: {浏览器 UA}`

3. **图像获取流程**：
   - 从 ARK URL 提取图像 ID（正则：`ark:/(?:[A-z0-9-_:]+)/([A-z\d-_:]+)`）
   - 从页面 HTML 提取 `SERVER_DATA.baseUrl` 和 `SERVER_DATA.sgBaseUrl`（图像存储服务器域名，如 `sg30p0.familysearch.org`）
   - POST 请求 `/search/filmdatainfo/image-data` 获取 DeepZoom 模板和图像列表
   - 图像使用 DeepZoom 瓦片格式：`{sgBaseUrl}/service/records/storage/deepzoomcloud/dz/v1/{id}/image.xml`
   - 瓦片 URL 格式：`{ServerBaseURL}/{URL}_files/{Level}/{X}_{Y}.jpg`

4. **请求类型**：
   - `image-data`：获取 DGS 号、图像 URL、Waypoint 信息
   - `film-data`：获取 DeepZoom 模板和图像列表

### 注意事项

- 需要有效的 FamilySearch 登录 session
- 图像来自缩微胶片数字化，使用 DeepZoom 瓦片技术提供
- 部分图像受地域或权限限制，可能需要在 FamilySearch 家族史中心才能访问
- FamilySearch 近期暂停了部分中文族谱访问权限，下载可能受影响

### 相关源码

- bookget FamilySearch 模块：https://github.com/deweizhu/bookget/blob/main/app/familysearch.go
- bookget wiki 说明：https://github.com/deweizhu/bookget/wiki/04.%E5%8F%AF%E7%94%A8%E7%9A%84%E7%BD%91%E7%AB%99URL
