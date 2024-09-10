
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

# Spire.pdf
## Install
```sh
pip install spire.pdf
```

## Usage
```python
from spire.pdf import PdfDocument
from spire.pdf import PdfTextExtractOptions
from spire.pdf import PdfTextExtractor

pdf = PdfDocument()
pdf.LoadFromFile(input_pdf_path)

extract_options = PdfTextExtractOptions()
extract_options.IsSimpleExtraction = True # if False, keep layout

texts = []
for i in range(pdf.Pages.Count):
    page = pdf.Pages.get_Item(i)
    text_extractor = PdfTextExtractor(page)
    text = text_extractor.ExtractText(extract_options)
    texts.append(text)
```

## Output
Outputs of `spire.pdf` are in [here](./output/spire_text.txt) for text format.

なぜかページが途中で切れてる。。。
結果、不採用。

# 検証結果
|  Method  |  Rank  |
| ---- | ---- |
|  PyMuPDF (Markdown)  | 1 |
|  PyMuPDF (Text)  | 2 |
|  LangChain DirectoryLoader (Text) | 3 |
|  spire.pdf  | 4 |

全体を通して、文字は完璧に抽出可能だが、表は微妙。