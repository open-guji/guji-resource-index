# FamilySearch - 家譜圖像

<!--
  本文件分两部分：
  - 分割线以上：用户文档，面向普通用户，语言简洁易懂，不含技术细节
  - 分割线以下：开发者文档，面向程序员，包含 API、HTML 解析、下载逻辑等技术细节
-->

FamilySearch（家谱搜索）的"家譜圖像"（Genealogy Images）是一个独立于"中國族譜收藏"的图像浏览合集，收录了来自中国各地的家谱缩微胶片数字化图像。与"中國族譜收藏"侧重于按姓氏和地点组织浏览不同，本合集更侧重于提供原始图像的直接浏览入口，用户可通过 FamilySearch 的图像搜索功能按地点和记录类型检索。

- 网站链接：https://www.familysearch.org/search/image/index?owc=https://www.familysearch.org/service/cds/recapi/sord/collection/2037955/waypoints
- 分享协议：免费访问，需注册账号；部分图像仅限 FamilySearch 家族史中心现场查看
- 资源类型：家谱缩微胶片数字化图像
- 不支持 IIIF 协议
- bookget 支持下载（与"中國族譜收藏"使用相同的下载机制）

## 搜索与浏览

**需要注册免费账号并登录后才能查看图像。**

### 通过图像搜索访问

1. 登录 https://www.familysearch.org
2. 点击顶部导航"搜索"（Search） > "图像"（Images）
3. 在"地点"（Place）字段输入"China"或具体省份名称
4. 当提示是否使用中文家谱搜索时，选择"否"（No）可查看所有记录类型（包括本合集）
5. 在右侧面板选择"所有记录类型"（All Record Types）
6. 利用搜索字段进一步筛选，点击"更新"（Update）

### 集合浏览页

- 浏览入口：https://www.familysearch.org/search/image/index?owc=https://www.familysearch.org/service/cds/recapi/sord/collection/2037955/waypoints
- 按层级目录结构组织，逐级点击展开浏览

### 与"中國族譜收藏"的区别

| 对比项 | 中國族譜收藏 (1787988) | 家譜圖像 (2037955) |
|--------|----------------------|-------------------|
| 合集 ID | 1787988 | 2037955 |
| 时间跨度 | 1239-2014 年 | 待确认 |
| 图像数量 | 1,300 万+ | 待确认 |
| 组织方式 | 按姓氏 → 国家 → 省 → 县 | 按目录层级 |
| 专用搜索 | 有族谱专用搜索界面 | 无，通过通用图像搜索 |
| 索引状态 | 纯图像浏览，未建索引 | 纯图像浏览，未建索引 |

两个合集可能存在部分内容重叠，但组织方式和入口不同。

### 注意事项

- 本合集同样为**纯图像浏览**（browse-only），无人名索引
- FamilySearch 近期因隐私法规审查暂停了部分中文家谱的访问权限，部分图像可能暂时不可用

## 每本书能看到什么

| 字段 | 说明 | 示例 |
|------|------|------|
| 书名 | 家谱名称（如有） | 待确认 |
| 胶片号 | 缩微胶片编号 | 待确认 |
| DGS 号 | 数字化图像组编号 | 待确认 |
| 图像数 | 该册图像总页数 | 待确认 |

- 可在线逐页翻阅扫描图像
- 无 PDF 下载功能
- 无全文文字（OCR）
- 图像来源于缩微胶片数字化

> 注：由于 FamilySearch 近期暂停了部分中文家谱访问，本合集的具体元数据字段有待实际访问后确认。

## 示例

- 浏览页面：https://www.familysearch.org/search/image/index?owc=https://www.familysearch.org/service/cds/recapi/sord/collection/2037955/waypoints
- 单张图像示例（通用格式）：https://www.familysearch.org/ark:/61903/3:1:3QSQ-G991-F9SJ

---

# 开发者文档

## URL 结构

### Waypoints 浏览页
```
https://www.familysearch.org/search/image/index?owc=https://www.familysearch.org/service/cds/recapi/sord/collection/2037955/waypoints
```
- `2037955`：本合集的 Collection ID

### 单张图像（ARK 标识符）
```
https://www.familysearch.org/ark:/61903/3:1:{image_id}
```
- 格式与"中國族譜收藏"完全一致
- `61903`：FamilySearch 的 ARK NAAN
- `3:1:{image_id}`：图像唯一标识
- 查询参数不影响图像获取

## 搜索 API

### Waypoints API

```
GET https://www.familysearch.org/service/cds/recapi/sord/collection/2037955/waypoints
```

返回合集的顶层导航节点，逐级展开获取下级节点。

FamilySearch 的 waypoints API 文档可参考其开发者中心：
- https://www.familysearch.org/developers/docs/api/records/Read_Waypoint_usecase

### 通用图像搜索

通过 FamilySearch 的图像搜索功能可跨合集检索：
```
https://www.familysearch.org/search/image/index?owc=...
```

无独立的结构化搜索 API 文档公开。

## 元数据获取

本合集为纯图像浏览型，元数据获取方式与"中國族譜收藏"一致：

### 1. Waypoints 导航树
通过逐级请求 waypoints API 获取层级结构。

### 2. 目录交叉查询
部分图像可通过 FamilySearch 目录（Catalog）的胶片号交叉查询获取书目信息：
```
GET https://www.familysearch.org/search/catalog/results?count=20&query=%2Bfilm_number%3A{胶片号}
```

### 字段映射

| 中文字段 | 提取方式 |
|---------|---------|
| 书名 | Waypoint 导航层级 / Catalog 交叉查询 |
| 胶片号 | Waypoint 节点属性 / 图像查看器页面 |
| DGS号 | 图像查看器页面 / Catalog 页面 |

## 下载

本合集的下载机制与"中國族譜收藏"完全一致，均通过 bookget 的 `familysearch.go` 模块处理。

### bookget 支持

**支持的 URL 格式（2025 年 2 月 13 日后仅此一种）：**
```
https://www.familysearch.org/ark:/61903/3:1:{image_id}
```

**关键技术细节：**

1. **认证方式**：需要 FamilySearch 账号的 `fssessionid` Cookie
   - 从 cookie 文件提取 `fssessionid`
   - 转换为 Bearer Token：`Authorization: bearer {fssessionid}`

2. **必需的 HTTP 请求头**：
   - `Authorization: bearer {fssessionid}`
   - `Cookie: {完整 cookie 字符串}`
   - `Origin: https://www.familysearch.org`
   - `Referer: https://www.familysearch.org/`
   - `User-Agent: {浏览器 UA}`

3. **图像获取流程**：
   - 从 ARK URL 提取图像 ID（正则：`ark:/(?:[A-z0-9-_:]+)/([A-z\d-_:]+)`）
   - 从页面 HTML 提取 `SERVER_DATA.baseUrl` 和 `SERVER_DATA.sgBaseUrl`
   - POST 请求 `/search/filmdatainfo/image-data` 获取 DeepZoom 模板和图像列表
   - DeepZoom 瓦片格式：`{sgBaseUrl}/service/records/storage/deepzoomcloud/dz/v1/{id}/image.xml`
   - 瓦片 URL：`{ServerBaseURL}/{URL}_files/{Level}/{X}_{Y}.jpg`

4. **与"中國族譜收藏"的技术共通性**：两个合集在 FamilySearch 后端使用相同的图像存储和分发基础设施，bookget 无需区分合集 ID，仅需单张图像的 ARK URL 即可下载。

### 注意事项

- 需要有效的 FamilySearch 登录 session
- 部分图像受地域或权限限制
- FamilySearch 近期暂停了部分中文家谱访问权限，下载可能受影响
- 批量遍历需通过 waypoints API 逐级获取图像列表

### 相关源码

- bookget FamilySearch 模块：https://github.com/deweizhu/bookget/blob/main/app/familysearch.go
- bookget wiki 说明：https://github.com/deweizhu/bookget/wiki/04.%E5%8F%AF%E7%94%A8%E7%9A%84%E7%BD%91%E7%AB%99URL
- FamilySearch 开发者 API 文档：https://www.familysearch.org/developers/docs/api/records/Read_Waypoint_usecase
