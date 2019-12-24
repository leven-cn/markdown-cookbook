# Python-Markdown

Refer to [Python-Markdown Documentation](https://python-markdown.github.io/)

## Features 特性

- International (**Unicode**) Support 支持国际化
- Output Format: `HTML5` and `XHTML` support 支持`HTML5`, `XHTML`输出格式
- Extention Support 支持扩展
- Command Line Interface 命令行

## Installation 安装

```bash
python3 -m pip install markdown
```

## Usage 用法

```python
import markdown

text = 'markdown file content'
output = markdown.markdown(text)
assert isinstance(output, str)

# Determine output format, "xhtml" by default
# 定义输出格式，默认"xhtml"
output = markdown.markdown(text, output_format='html5')

# Determine length of tabs, 4 by default
# 定义Tab缩进, 默认4
output = markdown.markdown(text, output_format='html5', tab_length=4)

# Input from Markdown file, output to a HTML-5 file
# 文件输入输出
input_file = 'example.md'
output_file = 'example.html'
markdown.markdownFromFile(input_file, output_file)
```

### Extensions Usage 使用插件

```python
import markdown

text = 'markdown file content'
output = markdown.markdown(text, extensions=['extra'])
output = markdown.markdown(text, extensions=['extra'], extension_configs = {
    'extra': {
        'option': 'value',
    }
})
```

Custom Extension 自定义插件

```python
import markdown
from markdown.extensions import Extension

class MyExtClass(Extension):
    pass
    # define your extension here...


text = 'markdown file content'
output = markdown.markdown(text, extensions=[MyExtClass(option='value')])
```

### Multiple Processing 批量处理

```python
import markdown

# Process multiple texts
# 批量处理多个文本
md = markdown.Markdown(output_format='html5', tab_length=4)
md.convert(text1)
md.reset().convert(text2)

# Process multiple files
# 批量处理多个文件
md = markdown.Markdown(output_format='html5', tab_length=4)
md.convertFile(input_file1, output_file1)
md.reset().convertFile(input_file1, output_file1)
```

## Extensions 扩展

### Official Extensions 官方扩展

| Extension 扩展 | Entry Point 参数调用名 |
| ------------- | ----------- |
| **Extra** | extra|
| &nbsp;&nbsp;&nbsp; **Abbreviations** | abbr |
| &nbsp;&nbsp;&nbsp; **Attribute Lists** | attr_list |
| &nbsp;&nbsp;&nbsp; **Definition Lists** | def_list |
| &nbsp;&nbsp;&nbsp; **Fenced Code Blocks** | fenced_code |
| &nbsp;&nbsp;&nbsp; Footnotes | footnotes |
| &nbsp;&nbsp;&nbsp; Tables | tables |
| **Admonition** | admonition |
| **CodeHilite** | codehilite |
| ~~Legacy Attributes~~ | ~~legacy_attr~~ |
| ~~Legacy Emphasis~~ | ~~legacy_em~~ |
| Meta-Data | meta |
| New Line to Break | nl2br |
| Sane Lists | sane_lists |
| SmartyPants | smarty |
| Table of Contents | toc |
| WikiLinks | wikilinks |

### Extra

```markdown
This is *true* markdown text.

<div markdown="1">
This is *true* markdown text.
</div>
```

Result:

```html
<p>This is <em>true</em> markdown text.</p>
<div>
<p>This is <em>true</em> markdown text.</p>
</div>
```

### Abbreviations 缩写

```markdown
The HTML specification
is maintained by the W3C.

*[HTML]: Hyper Text Markup Language
*[W3C]:  World Wide Web Consortium
```

will be rendered as:

```html
<p>The <abbr title="Hyper Text Markup Language">HTML</abbr> specification
is maintained by the <abbr title="World Wide Web Consortium">W3C</abbr>.</p>
```

### Attribute Lists 属性列表

```markdown
{: #id1 .class1 .class2 key='value' }
```

A word which starts with a hash (`#`) will set the id of an element.

A word which starts with a dot (`.`) will be added to the list of class
