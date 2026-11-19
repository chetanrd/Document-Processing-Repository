# document-processing-toolkit

A lightweight open-source Python toolkit for local document extraction, text normalisation, file fingerprinting and duplicate detection.

## Purpose

This utility provides a simple foundation for local document processing workflows, including:

- Extracting text from PDF and plain-text files
- Normalising whitespace and cleaning extracted text
- Computing SHA-256 fingerprints for file integrity verification
- Detecting duplicate files within a directory
- Extracting basic file metadata

## Problem Addressed

When working with document collections, it's often necessary to:

1. Extract text content for further processing or search
2. Verify file integrity through cryptographic hashes
3. Identify and remove duplicate files
4. Obtain basic file metadata without heavyweight dependencies

This toolkit addresses these needs with a minimal, dependency-light Python package that runs entirely locally.

## Features

- **Text extraction** from PDF (via pypdf) and TXT files
- **Text normalisation** (whitespace collapsing, Unicode normalisation)
- **SHA-256 fingerprinting** for file integrity and deduplication
- **Duplicate detection** within a directory tree
- **File metadata extraction** (size, modification time, extension, hash)
- **JSON output** for programmatic consumption
- **Single-file and batch-directory processing**
- **Zero external services** — runs completely offline

## Installation

```bash
pip install -r requirements.txt
```

Or install as a package:

```bash
pip install -e .
```

## Usage

### Process a single file

```bash
python -m document_toolkit path/to/file.pdf
python -m document_toolkit path/to/file.txt
```

### Process all supported files in a directory (recursive)

```bash
python -m document_toolkit path/to/directory --recursive
```

### Output as JSON

```bash
python -m document_toolkit path/to/file.pdf --json
python -m document_toolkit path/to/directory --recursive --json
```

### Find duplicates in a directory

```bash
python -m document_toolkit path/to/directory --duplicates
python -m document_toolkit path/to/directory --duplicates --json
```

### Combine options

```bash
python -m document_toolkit path/to/directory --recursive --duplicates --json
```

## Example JSON Output

### Single file processing

```json
{
  "file": "example.txt",
  "path": "/absolute/path/to/example.txt",
  "size_bytes": 1024,
  "extension": ".txt",
  "modified": "2026-01-15T10:30:00",
  "sha256": "a1b2c3d4e5f6...",
  "text": "Extracted and normalised text content...",
  "text_length": 512
}
```

### Duplicate detection

```json
{
  "duplicates": [
    {
      "hash": "a1b2c3d4e5f6...",
      "files": [
        "/path/to/file1.txt",
        "/path/to/file2.txt"
      ]
    }
  ],
  "total_files_scanned": 10,
  "duplicate_groups": 1,
  "total_duplicates": 2
}
```

## Supported File Formats

| Format | Extension | Text Extraction |
|--------|-----------|-----------------|
| Plain Text | `.txt` | Yes (native) |
| PDF | `.pdf` | Yes (via pypdf) |

Other formats will return metadata only (no text extraction).

## Current Limitations

- **Early-stage project** — API and CLI may change
- PDF extraction quality depends on pypdf; scanned/image-only PDFs will not yield text
- No OCR support
- No support for DOCX, EPUB, or other formats (contributions welcome)
- Duplicate detection is based on exact SHA-256 matches only
- Single-threaded processing

## Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT License — see [LICENSE](LICENSE) for details.