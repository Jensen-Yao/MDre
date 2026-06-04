# MDre 图片渲染压力测试

这个文件用于测试 MDre 在 Markdown 预览、预览态编辑、打印以及 Android WebView 中的图片渲染能力。

重点覆盖：普通相对路径、带空格文件名、中文文件名、括号、`#`、Windows 绝对路径、`file://`、SVG 大图、HTML 图片标签、表格/列表中的图片，以及故意缺失的图片。

## 1. 标准相对路径图片

![普通相对路径 PNG](image-render-stress-assets/normal.png)

## 2. 常见特殊文件名路径

文件名包含空格：

![空格文件名 PNG](image-render-stress-assets/space name image.png)

文件名包含中文和空格：

![中文文件名 PNG](image-render-stress-assets/中文 图片.png)

文件名包含括号和空格：

![括号文件名 PNG](image-render-stress-assets/paren (1).png)

文件名包含 `#`：

![井号文件名 PNG](image-render-stress-assets/hash#image.png)

已经编码的空格路径：

![已编码空格 PNG](image-render-stress-assets/space%20name%20image.png)

## 3. Windows 路径与 file URL

Windows 绝对路径，使用反斜杠：

![Windows 绝对路径](C:\Users\18052\Documents\Codex\2026-06-02\goal-md-md-windows-obsidian-vorojar\outputs\image-render-stress-assets\space name image.png)

未编码空格和中文的 file URL：

![未编码 file URL](file:///C:/Users/18052/Documents/Codex/2026-06-02/goal-md-md-windows-obsidian-vorojar/outputs/image-render-stress-assets/中文 图片.png)

已编码空格的 file URL：

![已编码 file URL](file:///C:/Users/18052/Documents/Codex/2026-06-02/goal-md-md-windows-obsidian-vorojar/outputs/image-render-stress-assets/space%20name%20image.png)

## 4. SVG 尺寸与比例压力测试

超宽 SVG：

![超宽 SVG](image-render-stress-assets/wide-panorama.svg)

超长 SVG：

![超长 SVG](image-render-stress-assets/tall-strip.svg)

透明 SVG：

![透明 SVG](image-render-stress-assets/transparent-overlay.svg)

## 5. Markdown 中的 HTML 图片

HTML `img` 标签，路径包含空格：

<img src="image-render-stress-assets/space name image.png" alt="HTML 空格路径图片" width="240">

HTML `picture` 标签：

<picture>
  <source srcset="image-render-stress-assets/wide-panorama.svg" type="image/svg+xml">
  <img src="image-render-stress-assets/normal.png" alt="HTML picture fallback">
</picture>

## 6. 列表和表格中的图片

- 列表内图片，路径包含空格：
  ![列表空格路径](image-render-stress-assets/space name image.png)
- 列表内图片，路径包含 `#`：
  ![列表井号路径](image-render-stress-assets/hash#image.png)

| 测试场景 | 图片 |
| --- | --- |
| 普通路径 | ![表格普通图片](image-render-stress-assets/normal.png) |
| 空格路径 | ![表格空格图片](image-render-stress-assets/space name image.png) |
| SVG 图片 | ![表格 SVG 图片](image-render-stress-assets/transparent-overlay.svg) |

## 7. 预期破损图片测试

下面这一项故意指向不存在的文件。它应该显示 alt 文本或破损图片标记，但不应该导致页面布局崩溃。

![故意缺失的图片](image-render-stress-assets/missing image.png)

## 8. 代码块内图片语法不应渲染

下面的 Markdown 图片语法位于 fenced code block 中。它应该保持源码文本，不应该渲染成图片。

```md
![这行应该保持源码](image-render-stress-assets/space name image.png)
![file url 代码示例](file:///C:/Users/18052/Documents/Codex/2026-06-02/goal-md-md-windows-obsidian-vorojar/outputs/image-render-stress-assets/space name image.png)
```

## 9. 重复图片加载压力

![重复 1](image-render-stress-assets/normal.png)
![重复 2](image-render-stress-assets/space name image.png)
![重复 3](image-render-stress-assets/中文 图片.png)
![重复 4](image-render-stress-assets/paren (1).png)
![重复 5](image-render-stress-assets/hash#image.png)
![重复 6](image-render-stress-assets/wide-panorama.svg)
![重复 7](image-render-stress-assets/tall-strip.svg)
![重复 8](image-render-stress-assets/transparent-overlay.svg)

