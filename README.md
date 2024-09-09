
# MyMuPDF
GMPガイドラインを用いてテストを実施。
## Instal
```sh
pip install PyMuPDF, markdown, markdownify
```
## Usage
### Simple Usage
```python
import pymupdf
doc = pymupdf.open("guideline.pdf")
texts = []
for page in doc:
  texts.append(page.get_text())

with open('text_ver.txt', 'w', encoding="utf-8") as f:
    for text in texts:
      f.write(text)
```
### Usage for coversion pdf into markdown
```python
import pymupdf
from markdownify import markdownify as md

doc = pymupdf.open("guideline.pdf")
texts = []
for page in doc:
  texts.append(md(page.get_text()))

with open('markdown_ver.md', 'w', encoding="utf-8") as f:
    for text in texts:
      f.write(text)
```
## Output
Outputs of `PyMiPDF` are in [here](./output/text_ver.txt) for text format and in [here](./output/markdown_ver.md) for markdown format.
結果、ほぼ差異はない。

# LangChain  DirectoryLoader PDF
## Install
```sh
pip install typing-inspect==0.8.0 typing_extensions==4.5.0

```