# E国宝 (e-Museum)

<!--
  本文件分两部分：
  - 分割线以上：用户文档，面向普通用户，语言简洁易懂，不含技术细节
  - 分割线以下：开发者文档，面向程序员，包含 API、HTML 解析、下载逻辑等技术细节
-->

E国宝是日本国立文化财机构（National Institutes for Cultural Heritage）建设的文物高清影像数据库，收录了旗下四座国立博物馆和一座研究所所藏的国宝与重要文化财的高清图像，提供日语、英语、中文、韩语四种语言的解说。

- 网站链接：https://emuseum.nich.go.jp/
- 版权声明：所有数字内容版权归国立文化财机构及各收藏机构所有，未经许可不得复制或转载（无论商用或非商用）
- 收录文物涵盖国宝和重要文化财两个级别
- 资源类型：绘画、书法、雕塑、建筑、金属工艺、刀剑、陶瓷、漆器、纺织品、考古、历史资料、法隆寺宝物（共12大类）
- 支持 IIIF 协议（Presentation API 2.1.1 / Image API 2.1.1），可使用 [bookget](https://github.com/deweizhu/bookget) 等工具下载
- 另有 iOS 和 Android 客户端

## 收藏机构

- 东京国立博物馆（Tokyo National Museum）
- 京都国立博物馆（Kyoto National Museum）
- 奈良国立博物馆（Nara National Museum）
- 九州国立博物馆（Kyushu National Museum）
- 奈良文化财研究所（Nara National Research Institute for Cultural Properties）

## 搜索与浏览

- 搜索页面：https://emuseum.nich.go.jp/search?langId=zh
- 支持关键词搜索，也支持按以下字段高级搜索：名称、作者/产地/出土地
- 搜索结果可按以下维度筛选：
  - 分类：绘画、书法、雕塑、建筑、金属工艺、刀剑、陶瓷、漆器、纺织品、考古、历史资料、法隆寺宝物
  - 地域：日本、朝鲜、中国、其他
  - 时代：从绳文时代到近代（日本）、秦汉到清代（中国）等
  - 世纪：公元前～20世纪
  - 指定等级：国宝、重要文化财
  - 收藏馆：五个收藏机构可选
- 无需注册登录即可浏览和查看高清图像

## 每件文物能看到什么

| 字段 | 说明 | 示例 |
|------|------|------|
| 名称 | 文物名称 | 群书治要 |
| 分类 | 类别 | 书法 |
| 指定 | 文化财等级 | 国宝 |
| 时代 | 创作年代 | 平安时代 11世纪 |
| 形态/材质 | 材质与制作工艺 | 彩笺墨书 |
| 尺寸 | 尺寸信息 | 27.1x721.2~1472.7cm |
| 数量 | 卷/件数 | 13卷 |
| 收藏编号 | 馆藏编号 | B-2531 |
| 收藏机构 | 所属博物馆 | 东京国立博物馆 |
| 解说 | 详细的文物介绍与历史背景 | （长文） |

- 每件文物都配有高清图像浏览器（Deepviewer），支持缩放、全屏、键盘导航
- 图像下方有"IIIF Manifest"按钮，可获取 IIIF manifest 链接用于外部查看器
- 部分作品（如卷轴）支持连续浏览模式和从右到左的阅读方向
- 无 PDF 下载功能
- 无全文文字（OCR）

## 示例

- 群书治要（中文）：https://emuseum.nich.go.jp/detail?langId=zh&webView=&content_base_id=100168&content_part_id=0&content_pict_id=0
- 日本书纪 卷十（英文）：https://emuseum.nich.go.jp/detail?langId=en&webView=&content_base_id=100249&content_part_id=0&content_pict_id=0
- 传教大师笔尺牍 久隔帖：https://emuseum.nich.go.jp/detail?langId=zh&webView=&content_base_id=100243&content_part_id=001&content_pict_id=0

---

# 开发者文档

## URL 结构

### 详情页

```
https://emuseum.nich.go.jp/detail?langId={lang}&webView=&content_base_id={base_id}&content_part_id={part_id}&content_pict_id={pict_id}
```

- `langId`：语言代码，可选值 `ja`（日语）、`en`（英语）、`zh`（中文）、`ko`（韩语）
- `content_base_id`：作品基础 ID，如 `100168`
- `content_part_id`：部件/卷 ID，如 `0`、`001`、`009`
- `content_pict_id`：图片 ID，通常为 `0`
- `webView`：留空即可

### 搜索页

```
https://emuseum.nich.go.jp/search?langId={lang}
```

### 高级搜索

```
https://emuseum.nich.go.jp/search?langId={lang}&d_lang=ja&s_temp={keyword}&s_title={title}&s_author={creator}
```

### IIIF Manifest

```
https://emuseum.nich.go.jp/iiifapi/{book_id}/manifest.json
```

- `book_id` 由 `content_base_id` + 零填充的 `content_part_id` 拼接而成
- 例如：base_id=`100243`，part_id=`001` => book_id=`100243001`
- 例如：base_id=`100168`，part_id=`0` => book_id=`100168000`（part_id 不足3位时前补零）

### IIIF 图片

```
https://emuseum.nich.go.jp/iiif/?IIIF=/{filename}.tif/full/full/0/default.jpg
```

- `filename` 格式为 `{book_id}{序号}`，如 `100243001002`
- 支持标准 IIIF Image API 2.0 Level 1 参数：`/{region}/{size}/{rotation}/{quality}.{format}`

## 搜索 API

网站为服务端渲染（jQuery 增强），搜索结果直接在 HTML 中返回。无公开的 JSON 搜索 API。需通过页面 HTML 解析搜索结果。

搜索请求为 GET 请求，参数如下：

| 参数 | 说明 | 示例 |
|------|------|------|
| `langId` | 语言 | `zh` |
| `d_lang` | 数据语言 | `ja` |
| `s_temp` | 关键词 | `群书治要` |
| `s_title` | 名称 | |
| `s_author` | 作者/产地 | |

筛选参数（待确认具体参数名）：
- 分类、地域、时代、世纪、指定等级、收藏馆

## 元数据获取

网站采用服务端渲染（SSR），元数据直接嵌在 HTML 页面中，可直接解析 HTML 提取。

也可通过 IIIF Manifest 获取基础元数据（label 字段包含多语言标题）。

### 从 HTML 详情页提取

详情页为标准 HTML，元数据在页面正文中渲染。具体 CSS 选择器待确认（需实际解析页面 DOM 结构），但整体为表格/列表形式展示各字段。

### 从 IIIF Manifest 提取

```
GET https://emuseum.nich.go.jp/iiifapi/{book_id}/manifest.json
```

响应为标准 IIIF Presentation API 2.1.1 格式：

```json
{
  "label": "作品名称（多语言）",
  "sequences": [
    {
      "canvases": [
        {
          "label": "1",
          "width": 5000,
          "height": 3750,
          "images": [
            {
              "resource": {
                "@id": "https://emuseum.nich.go.jp/iiif/?IIIF=/{filename}.tif/full/full/0/default.jpg",
                "service": {
                  "@id": "https://emuseum.nich.go.jp/iiif/?IIIF=/{filename}.tif"
                }
              }
            }
          ]
        }
      ]
    }
  ]
}
```

### 字段映射

| 中文字段 | 提取方式 |
|---------|---------|
| 名称 | IIIF Manifest `label` / HTML 详情页标题区域 |
| 图片列表 | IIIF Manifest `sequences[0].canvases[*].images[0].resource.@id` |
| 图片服务 | IIIF Manifest `sequences[0].canvases[*].images[0].resource.service.@id` |
| 其他元数据 | HTML 详情页解析（分类、时代、材质、尺寸、收藏机构等） |

## 下载

### IIIF 下载（推荐）

eMuseum 完整支持 IIIF，这是获取高清图像的首选方式。

**Manifest URL 构建规则：**

1. 从详情页 URL 提取 `content_base_id` 和 `content_part_id`
2. 将 `content_part_id` 零填充至3位（不足3位前补 `0`）
3. 拼接为 `book_id = content_base_id + content_part_id_padded`
4. Manifest URL: `https://emuseum.nich.go.jp/iiifapi/{book_id}/manifest.json`

**从 Manifest 到图片 URL：**

1. 解析 manifest JSON，遍历 `sequences[0].canvases`
2. 每个 canvas 的 `images[0].resource.service.@id` 即为 IIIF Image API service 端点
3. 拼接完整图片 URL：`{service_id}/full/full/0/default.jpg`（原始尺寸）
4. 或指定尺寸：`{service_id}/full/{width},/0/default.jpg`

**注意：** IIIF Image API service 的 `@id` 格式为：
```
https://emuseum.nich.go.jp/iiif/?IIIF=/{filename}.tif
```

### bookget 支持

bookget 已内置 eMuseum 支持。

- 源码：https://github.com/deweizhu/bookget/blob/main/app/emuseum.go
- 用法：
  ```
  bookget "https://emuseum.nich.go.jp/detail?content_base_id=100168&content_part_id=009&langId=zh&webView="
  ```
  或直接使用 manifest URL：
  ```
  bookget "https://emuseum.nich.go.jp/iiifapi/100243001/manifest.json"
  ```

**bookget 关键逻辑：**

1. 从详情页 URL 用正则 `content_base_id=([A-z0-9]+)&content_part_id=([A-z0-9]+)` 提取 ID
2. `content_part_id` 不足3位时前补 `00` 拼接为 `book_id`
3. 获取详情页 HTML，用正则 `https://(.+)/manifest.json` 提取 manifest URL
4. 请求 manifest JSON，解析 canvases 获取图片列表
5. 支持两种下载模式：
   - 普通模式：直接下载 `{service_id}/full/full/0/default.jpg`
   - Dezoomify 模式：通过 `{service_id}/info.json` 获取分块信息后拼接高清大图
6. 文件名格式：`%04d.jpg`（从0001开始）

**必需的 HTTP 请求头：**

| Header | 值 |
|--------|---|
| `User-Agent` | 可配置（默认 bookget UA） |
| `Referer` | 详情页 URL（需 URL encode） |

### 图片保护

- 无水印
- 无 Token/Cookie 认证要求
- 需设置 Referer 头
- IIIF Image API 支持 Level 1，支持缩放、裁切、旋转等标准操作
