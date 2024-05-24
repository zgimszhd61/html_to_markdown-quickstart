# html_to_markdown-quickstart

```
from markdown_pdf import MarkdownPdf, Section
import requests
import html2text

# 定义一个函数，接收网页的URL作为参数
def html_to_markdown(url):
    # 使用requests获取网页内容
    response = requests.get(url)
    # 确保请求成功
    if response.status_code == 200:
        # 获取网页的HTML内容
        html_content = response.text
        # 创建html2text对象
        h = html2text.HTML2Text()
        # 修改此处：不再忽略链接，同时确保图片也被转换
        h.ignore_links = False
        h.ignore_images = False
        # 使用html2text将HTML转换为Markdown
        markdown_content = h.handle(html_content)
        # 返回转换后的Markdown内容
        return markdown_content
    else:
        return "请求网页失败，状态码：" + str(response.status_code)

# 使用函数转换指定的URL
url = "https://baoyu.io/translations/anthropic/mapping-mind-language-model"  # 替换为你想转换的网页的URL
markdown_content = html_to_markdown(url)
print(markdown_content)

# 创建MarkdownPdf实例
pdf = MarkdownPdf()

# 将Markdown内容添加到PDF中。这里使用Section类来包装Markdown内容。
pdf.add_section(Section(markdown_content))

# 设置PDF文档的元数据
pdf.meta["title"] = "Markdown转PDF示例"
pdf.meta["author"] = "作者名"

# 保存PDF文件。指定文件名和路径。
pdf.save("new_markdown-02.pdf")
```
