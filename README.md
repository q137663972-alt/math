# 数学乐园（Math Playground）

小学 1–6 年级数学练习 H5 / 安卓 APK。口算竖式、乘法口诀、应用题、图形单位分数，题目无限刷新。

## 玩法（9 种）

| 玩法 | 说明 |
| --- | --- |
| 口算练习 | 8 道题闯关，按年级出加减乘除 |
| 限时口算 | 60 秒速算连击 |
| 竖式填空 | 竖式里缺了谁？（缺数 / 缺运算符号） |
| 口诀接龙 | 乘法口诀张口就来 |
| 应用题闯关 | 240 道生活应用题（分年级带思路提示） |
| 图形分类 | 认图形、数边数棱数（13 种图形矢量配图） |
| 单位换算 | 米厘米、元角分、千克克、升毫升 |
| 分数比大小 | 分数比较 / 涂色部分占几分之几（SVG 图示） |
| 综合挑战 | 口算 + 图形 + 单位 + 分数大混战 |

## 内容规模

- **44 个参数化出题器**（`js/gen.js`），按年级配置，题目无限生成
- **240 道应用题**、32 条单位换算、13 种图形（内联 SVG 配图）
- 竖式、分数涂色图、图形配图全部矢量绘制，电视大屏不糊

## 目录结构

```
index.html / css/ / js/          H5 本体（纯静态，无构建）
math-app/                        电视版壳（横屏 + 遥控器焦点 + LEANBACK_LAUNCHER）
math-phone/                      手机版壳（竖屏 + 触屏交互）
.github/workflows/build.yml      CI：出 APK + 部署 GitHub Pages
```

## 在线版

<https://q137663972-alt.github.io/math/>

手机浏览器打开即可玩，数据存在本机 localStorage（`math_` 前缀），不上传服务器。

## 本地运行

```bash
python3 -m http.server 8892
# 浏览器打开 http://127.0.0.1:8892/index.html
```

## 构建 APK

推送到 GitHub 后 Actions 自动构建；也可手动 `workflow_dispatch`。
产物在 Release（临时）与 Actions Artifacts 中：

- `MathPlayground-TV.apk`（电视版）
- `MathPlayground-Phone.apk`（手机版）

## 出题器结构

`js/data-m1.js … data-m6.js` 按年级挂载单元配置：
`(function(g){ (window.GRADES=window.GRADES||[]).push(g); })({g:1, books:[{n:"一上册", u:[{n:"20以内加减法", k:"➕", gen:[{"t":"addsub20"}]}]}]})`

`js/gen.js` 里 `GEN.<名称>(cfg)` 返回 `{ q 题面, a 答案, opts 选项, say 朗读, v 竖式数据, img 配图 }`。
`js/data-extra.js` 提供图形表 `SHAPES`（含矢量图 `SHAPE_SVG`）、单位换算 `UNITS`、应用题 `APPQ`。
