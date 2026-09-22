# CBETA 电子佛典

CBETA（原「中华电子佛典协会」，2023 年 8 月起由「財團法人佛教電子佛典基金會」接续全部业务）以《大正新脩大藏經》《卍新纂續藏經》《嘉興大藏經》等刊本为底本，逐字录入、校勘并加新式标点，形成汉文佛典电子全文；由台湾法鼓文理学院（DILA）提供在线阅读平台 CBETA Online 与开放 API，原始 XML 数据公开在 GitHub 上。它是文本整理成果，不是藏经原件的收藏机构，引用时宜同时注明所据刊本（如「大正藏第 8 册 No. 251」）。

- 网站链接：https://www.cbeta.org/ （在线阅读：https://cbetaonline.dila.edu.tw/ ）
- 分享协议：[CBETA 版权宣告](https://www.cbeta.org/copyright)——限非营利使用；未特别说明者采用 CC BY-NC-SA 4.0；《印順法師佛學著作集》《呂澂佛學著作集》《太虛大師全書》《演培法師全集》不适用 CC 授权
- 规模：2026.R2 版共 4,899 部、22,150 卷（不含序言、目录等非本文则为 4,783 部、22,021 卷），约 2.29 亿个汉字，涵盖 26 种藏经与文献集（出处：[CBETA API 统计](https://cbdata.dila.edu.tw/stable/download/stat/stat-all.json)，2026-09 核实）
- 主要部分：《大正藏》2,457 部 8,982 卷、《卍續藏》1,230 部 5,065 卷、《嘉興藏》285 部 1,659 卷、《大藏經補編》164 部 1,429 卷；另有《趙城金藏》《高麗藏》《永樂北藏》《乾隆藏》《房山石經》《洪武南藏》、国家图书馆善本佛典、《漢譯南傳大藏經》《藏外佛教文獻》、佛寺志，以及印顺、太虚、吕澂、演培等近代著作集
- 资源类型：汉文佛典校勘全文（带新式标点与校勘记）；部分藏经可对照原书影像
- 部分藏经的原书影像（《大正藏》、国家图书馆善本佛典、佛寺志等）支持 IIIF 协议；全文可免费下载为纯文本、HTML、EPUB、PDF 等格式

## 搜索与浏览

- 在线阅读与检索：https://cbetaonline.dila.edu.tw/ （有繁体、简体、英文界面）
- 左侧「目录」可按藏经（大正藏、卍續藏、嘉興藏……）逐册、逐部浏览，也可按 CBETA 自订的部类目录（般若部类、华严部类……）浏览
- 可按经名、经号查找，也可做全文检索（查一个词出现在哪些经、哪一卷哪一行）；还可按作译者、朝代或公元年代筛选检索范围
- 另附词典、人名规范资料、相似句检索等辅助功能
- 阅读和检索无需注册登录；页面嵌有 Cloudflare 人机验证组件，部分操作前会先验证（具体是哪些功能待确认）
- 离线使用：官网「下载电子佛典集成」提供阅读软件与电子书下载

## 每本书能看到什么

| 字段 | 说明 | 示例 |
|------|------|------|
| 经号 | CBETA 编号（藏经代码 + 经号） | T0251 |
| 经名 | 典籍名称 | 般若波羅蜜多心經 |
| 藏经与册 | 所据刊本及册次 | 大正新脩大藏經 第 8 冊 |
| 卷数 | 全经卷数 | 1 卷 |
| 作译者 | 撰者或译者（带朝代） | 唐 玄奘譯 |
| 部类 | CBETA 部类 / 原藏经部别 | 般若部類 / 般若部 |
| 年代 | 译出或成书年代 | 648–649 |
| 行首 | 对应原书的页、栏、行 | T08n0251_p0848a01（第 848 页上栏第 1 行） |
| 校勘记 | 原书与 CBETA 的校勘注 | 帝【大】，諦【宋】【元】【明】 |
| 版本记录 | 本数据的发行与更新日期、底本及录入来源 | 發行日期：2026-08，最後更新：2025-07-27 |

- 在线阅读的是经过校勘、加了新式标点的文字，不是影印原书；每行都标出对应原书的页码与行号，便于回查纸本
- 有原书影像的藏经，正文中会显示一个影像按钮，点开可看对应页的扫描图（目前实测可用的有《大正藏》、国家图书馆善本佛典、《中國佛寺史志彙刊》等；《高麗藏》跳转到韩国东国大学的影像站）。《卍續藏》《嘉興藏》等未见影像
- 可下载单部佛典的纯文本、HTML、EPUB、PDF、DOCX、ODT，也可一次下载全部
- 阅读设置中可切换是否显示标点、行首、校勘，以及是否按原书换行；原书无标点的部分可选显示 AI 标点（站方注明由古籍酷 AI 标点引擎提供）；有「引用複製」功能

## 示例

- 《般若波羅蜜多心經》（唐玄奘译，T0251）：https://cbetaonline.dila.edu.tw/zh/T0251_001
- 《金剛般若波羅蜜經》（后秦鸠摩罗什译，T0235）：https://cbetaonline.dila.edu.tw/zh/T0235_001
- 《心经》所在原书页影像（大正藏第 8 册第 848 页）：https://dia.dila.edu.tw/uv3/index.html?id=Tv08p0848

---

# 开发者文档

以下均为 2026-09-22 实测（CBETA API 4.6.7，数据版本 2026R2）。

## URL 结构

### 编号体系

- **经号 `work`**：藏经代码 + 经号，如 `T0251`、`X1234`、`J0123`（藏经代码表见 [藏經代碼說明](https://www.cbeta.org/format/id.php)，现跳转至 archive2.cbeta.org）
- **文件号 `file`**：藏经代码 + 册 + `n` + 经号，如 `T08n0251`（大正藏第 8 册第 251 号）
- **行首 `lb`**：`{file}_p{页}{栏}{行}`，如 `T08n0251_p0848a01`；栏为 `a/b/c`（上中下栏）
- 前端的 `String.prototype.toRay` 把 `T08n0251` 转成 `T0251`（去掉册号部分）

### 阅读页（SPA）

```
https://cbetaonline.dila.edu.tw/{lang}/{work}_{juan}
```
- `lang`：`zh`（繁）、`zh-cn`、`zh-tw`、`en`
- `work`：经号，如 `T0251`
- `juan`：三位补零的卷号，如 `001`；省略时前端默认第 1 卷
- 服务器对任意路径都返回同一个 64 KB 的 SPA 外壳（`<title>CBETA 線上閱讀`），正文由前端调用 CBETA API 取得，curl 抓页面拿不到经文

### 藏经目录

```
https://cbetaonline.dila.edu.tw/mulu/{canon}
```
- `canon`：`T`、`X`、`J`、`B`、`D`、`GA` 等

### 原书影像查看器

```
https://dia.dila.edu.tw/uv3/index.html?id={canon}v{vol}{page}
```
- 例：`Tv08p0848` = 大正藏第 8 册第 848 页；`GAv015pa036a` 之类也合法
- 查看器（Universal Viewer 3）只接受 `^(D|GA|GB|JM|T)(v\d+)([apz][ab\d]\d+a?)$`，可推知自建影像限于这几种代码（实测 T、D、GA 的 manifest 可取；GB、JM 未测，JM 所指藏经待确认）
- 阅读页 HTML 中以 `<a class="facsimile" data-canon="T" data-ref="Tv08p0848">` 标出影像页；`data-s="dongguk"` 的（高丽藏）改跳 `https://kabc.dongguk.edu/viewer/view?dataId=ABC_IT_...`

## 搜索 API

CBETA API：https://cbdata.dila.edu.tw/stable/ （文档即此页，源码 [DILA-edu/cbeta-api](https://github.com/DILA-edu/cbeta-api)）。无需认证，官方要求调用时设置 HTTP `Referer` 头以便统计。全部 GET，返回 JSON。

| 端点 | 用途 | 实测示例 |
|------|------|---------|
| `works?work={work}` | 单部佛典元数据 | `works?work=T0251` |
| `search/title?q={词}` | 经名检索 | `search/title?q=心經` → `num_found: 141` |
| `search?q={词}&rows={n}` | 全文检索（按卷返回命中） | `search?q=觀自在菩薩&rows=2` → `num_found: 718`，`total_term_hits: 2677` |
| `toc?q={词}` | 在部类目录与经名中查找 | `toc?q=心經` → `num_found: 299`，结果 `type` 为 `catalog` 或 `work` |
| `works/toc?work={work}` | 佛典内目次（品、卷） | `works/toc?work=T0235` |
| `juans?work={work}&juan={n}` | 取某卷 HTML 正文 | `juans?work=T0251&juan=1` |
| `health` | 健康检查 | 返回 `success` |

`search` 响应主要字段：`query_string`、`num_found`、`total_term_hits`、`results[]`（`work`、`juan`、`title`、`byline`、`canon`、`category`、`file`、`term_hits`、`creators_with_id`、`time_dynasty`、`time_from`、`time_to`、`juan_list`）。其他端点（按作译者、按时间、范围选择、中文工具、SHINE 等）见 API 首页各文档页。

## 元数据获取

用 `works` 端点。`GET https://cbdata.dila.edu.tw/stable/works?work=T0251` 的实测响应：

```json
{"num_found":1,"results":[{"work":"T0251","uuid":"d1e52ff2-1592-49c9-b31c-377c909bc41b",
 "canon":"T","category":"般若部類","orig_category":"般若部","vol":"T08",
 "title":"般若波羅蜜多心經","juan":1,"juan_list":"1","cjk_chars":1097,"en_words":0,
 "file":"T08n0251","juan_start":1,"byline":"唐 玄奘譯","creators":"玄奘",
 "creators_with_id":"玄奘(A000294)","time_dynasty":"唐","time_from":648,"time_to":649,
 "places":[{"name":"翠微寺","id":"PL000000042513","latitude":33.839563,"longitude":108.928138}]}]}
```

`works?work=T0235` 同构：`title` 金剛般若波羅蜜經、`byline` 後秦 鳩摩羅什譯、`creators_with_id` 鳩摩羅什(A001583)、`time_from/time_to` 402/412、`cjk_chars` 5191。

### 字段映射

| 中文字段 | JSON 路径（`works` 端点） |
|---------|---------|
| 经号 | `results[0].work` |
| 经名 | `results[0].title` |
| 藏经代码 | `results[0].canon` |
| 册 | `results[0].vol` |
| 文件号 | `results[0].file` |
| 卷数 | `results[0].juan`（卷号列表 `juan_list`） |
| 作译者（原书题署） | `results[0].byline` |
| 作译者（规范名） | `results[0].creators`；带人名规范 ID 的为 `creators_with_id`（ID 对应 DILA 人名规范库 authority.dila.edu.tw） |
| 朝代 | `results[0].time_dynasty` |
| 年代 | `results[0].time_from` – `time_to`（公元年） |
| 部类 | `results[0].category`（CBETA 部类）/ `orig_category`（原藏经部别） |
| 译经地点 | `results[0].places[].name`（含 `id`、经纬度） |
| 字数 | `results[0].cjk_chars` |

补充：

- **卷 HTML**：`juans` 返回 `results[0]` 为整卷 HTML 字符串，含行首 `<span class="lb" id="T08n0251_p0848a01">`、影像锚点 `<a class="facsimile" data-ref="Tv08p0848">`、校勘记 `<div class='footnote'>`，末尾 `<div id='cbeta-copyright'>` 给出「經文資訊 / 版本記錄 / 原始資料」
- **全部佛典卷列表**：`https://cbdata.dila.edu.tw/stable/download/all-works.json`（实测 5,748 条，每条 `work`、`title`、`juans[]`）
- **作译者列表**：`download/all-creators.json`、`download/all-creators-with-alias.json`（后者 `num_found: 2185`，含别名）
- **统计**：`download/stat/stat-all.json`（`total` 与 `by_canon` 两部分，字段 `works_all`、`juans_all`、`cjk_chars_all` 等）；按部 CSV 为 `download/stat/cbeta-word-count.csv`

### GitHub 原始数据

- [cbeta-org/xml-p5](https://github.com/cbeta-org/xml-p5)：CBETA 正式的 TEI P5 XML 经文（2019 年起的版本，默认分支 `master`；2019-01-08 之前的旧版在 `cbeta-org/xml-p5-2018`）。路径为 `{canon}/{canon}{vol}/{file}.xml`，例：
  - https://raw.githubusercontent.com/cbeta-org/xml-p5/master/T/T08/T08n0251.xml （14,712 字节）
  - https://raw.githubusercontent.com/cbeta-org/xml-p5/master/T/T08/T08n0235.xml
- XML 的 `teiHeader` 含：`titleStmt/title`（丛书名与经名，中英文）、`author`（唐 玄奘譯）、`publicationStmt/idno`（canon/vol/no）、`availability`（"Available for non-commercial use when distributed with this header intact."）、`sourceDesc/bibl`（底本）、`projectDesc`（录入与标点来源）、`tagsDecl` 中的校本略符（【大】【宋】【元】【明】……）
- [cbeta-org/cbeta_gaiji](https://github.com/cbeta-org/cbeta_gaiji)：缺字（gaiji）资料
- [DILA-edu/cbeta-documentation](https://github.com/DILA-edu/cbeta-documentation)：XML 格式与文件结构说明
- xml-p5 的 README 版权说明指向 CBETA 版权宣告页（其他仓库未逐一核对）；`cbeta-org` 下其他仓库本次未能列出（GitHub API 在本环境受限），待确认

## 下载

### 文本（CBETA API 下载区）

| 格式 | 单部 / 单卷 | 全部 |
|------|------------|------|
| 纯文本（不含校注） | `download/text/T0251.txt.zip`；单卷 `download/text/T0001_001.txt.zip` | `download/cbeta-text.zip` |
| 纯文本（含校注） | `download/text-with-notes/T0001.txt.zip` | `download/cbeta-text-with-notes.zip` |
| HTML | `download/html/A1057_001.html`；整部 `download/html/A1057.html.zip` | — |
| EPUB | `download/epub/{canon}/{work}.epub`，如 `download/epub/T/T0251.epub` | `download/cbeta-epub.zip` |
| PDF | `download/pdf/{canon}/{work}.pdf`，如 `download/pdf/T/T0251.pdf` | `download/cbeta-pdf-{1,2,3}.zip`（内含总目录 `filelist_2026R2.txt`） |
| DOCX / ODT | `download/{docx,odt}/{canon}/{work}.{ext}` | — |

以上路径前缀均为 `https://cbdata.dila.edu.tw/stable/`。实测：`epub/T/T0251.epub` 200（application/epub+zip，91,533 字节），`pdf/T/T0251.pdf` 200（395,305 字节），`text/T0251.txt.zip` 200（3,230 字节）。纯文本中的图以 `【圖：T16p0845_01.gif】` 标记，图档一并打包；悉昙字以罗马转写呈现。完整 XML 则直接 clone `cbeta-org/xml-p5`。

### 原书影像（IIIF）

- 支持 IIIF Presentation 2.0 与 Image API 2.0（level1），无需认证
- Manifest（一册一个）：`https://dia.dila.edu.tw/iiif/{canon}/v{vol}/manifest.json`
  - 实测 `T/v08` 200，932 个 canvas；`D/v01`、`GA/v001` 200；`X/v01`、`J/v01` 404（无影像）
  - 册号位数随藏经而异：T 为两位（`v08`），GA 为三位（`v001`）
  - manifest 中未见 `license`、`attribution`、`metadata` 字段
- 页 → canvas 序号：`https://dia.dila.edu.tw/pages/{id}/offset`，例 `pages/Tv08p0848/offset` → `{"result":859}`，canvas `label` 为 `p0848`
- Image service：`https://dia.dila.edu.tw/iiifimgs/{canon}/v{vol}/{canon}v{vol}{page}.tif`，例：
  - info.json：https://dia.dila.edu.tw/iiifimgs/T/v08/Tv08p0848.tif/info.json （原图 2145×3000）
  - 图片：https://dia.dila.edu.tw/iiifimgs/T/v08/Tv08p0848.tif/full/600,/0/default.jpg （实测 200，image/jpeg）
- 流程：`works` 取 `canon`/`vol` → 取 manifest → 遍历 `sequences[0].canvases[].images[0].resource.service['@id']` → 拼 `/full/full/0/default.jpg`
- bookget 是否已内置该站：待确认（标准 IIIF manifest，理论上可直接交给支持 IIIF 的工具）
- 影像的版权归属与再利用条款：CBETA 版权宣告未单独说明，待确认（《大正藏》著作权人为大藏出版株式會社）
