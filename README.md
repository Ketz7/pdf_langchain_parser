# PDF LangChain Parser

This project demonstrates a small pipeline for parsing PDF files and preparing their text for use with [LangChain](https://python.langchain.com/).

The code provides:

- **CustomPDFParser** – a class built on top of `pypdf` to extract text and metadata from PDF documents. It supports cleaning page text, removing repeated headers and footers, and optionally gathering basic image information.
- **LangChainPDFLoader** – a loader that converts the parsed pages into LangChain `Document` objects with metadata. It also offers optional chunking of large texts using `RecursiveCharacterTextSplitter`.
- **PDFProcessingPipeline** – a convenience wrapper exposing a single method to parse a PDF and return the result in different formats (raw data, plain text, or LangChain documents).
- **example.py** – a small interactive example that lets you parse a PDF and inspect the results from the command line.

## Installation

1. Install the required Python packages:

```bash
pip install -r requirements.txt
```

2. (Optional) create and activate a virtual environment before installing.

## Usage

### Running the example script

```
python src/example.py
```

The script will prompt for a PDF file path and show different ways to view the parsed content (raw data, plain text, or LangChain documents with optional chunking).

### Using the pipeline in your own code

```python
from pipeline import PDFProcessingPipeline

pipeline = PDFProcessingPipeline({
    "preserve_layout": False,
    "remove_headers_footers": True,
    "extract_images": True,
    "min_text_length": 20,
})

# Get LangChain documents split into chunks
chunks = pipeline.process_single_pdf("path/to/file.pdf", output_format="langchain")
```

See `src/parser.py` and `src/langchain_loader.py` for additional options and details.

## Repository structure

```
src/
├── parser.py            # CustomPDFParser implementation
├── langchain_loader.py  # LangChain loader and chunking logic
├── pipeline.py          # High level interface for parsing
├── example.py           # Interactive example script
└── Articles.pdf         # Sample PDF used for testing
```

## License

This repository is provided for demonstration purposes and has no explicit license.
