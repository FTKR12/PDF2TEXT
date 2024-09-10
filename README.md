
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
```
### Usage for coversion pdf into markdown
```python
import pymupdf
from markdownify import markdownify as md

doc = pymupdf.open("guideline.pdf")
texts = []
for page in doc:
  texts.append(md(page.get_text()))
```
## Output
Outputs of `PyMuPDF` are in [here](./output/pymupdf_text.txt) for text format and in [here](./output/pymupf_markdown.md) for markdown format.

結果、ほぼ差異はない。mdの方が若干構造化されている？

# LangChain  DirectoryLoader PDF
## Install
```sh
pip install langchain-community, pdfminer.six
```
## Usage
`PyPDFDirectoryLoader`では対応してない日本語フォントがあるらしいので`PDFMinerLoader`を使用。
```python
from langchain.document_loaders import PDFMinerLoader

loader = PDFMinerLoader(f'{input_pdf_dir}/guideline.pdf')
docs = loader.load()
texts = []
for doc in docs:
  texts.append(doc.page_content)
```
## Output
Outputs of `PDFMinerLoader` are in [here](./output/langchain_loader.txt) for text format.

結果、`PyMuPDF`の方が良さそう。