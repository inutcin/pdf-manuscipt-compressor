# pdfmanuc

## About

`pdfmanuc` (pdf manuscript compressor) is a CLI tool for compressing PDF files
of handwritten lecture notes.

Tablet software used for lecture recording produces very large PDF files even
though their content is black-and-white imagery of low density (more than 99%
of the area is a white background). `pdfmanuc` converts such documents into
monochrome form and repacks them, reducing the file size many times over
without a noticeable loss of readability on a tablet or computer screen.

The compression pipeline is:

```
pdf -> monochrome pbm -> per-page pdf -> single pdf
```

## Installation

### Clone the repository

```bash
git clone https://github.com/inutcin/pdf-manuscipt-compressor.git
cd pdf-manuscipt-compressor
```

### Install dependencies

The script requires `pdftoppm`, `img2pdf` and `pdftk`.

Ubuntu / Debian:

```bash
sudo apt update && sudo apt install -y poppler-utils img2pdf pdftk-java
```

Red Hat / Fedora:

```bash
sudo dnf install -y poppler-utils img2pdf pdftk
```

Arch Linux:

```bash
sudo pacman -S --needed poppler img2pdf pdftk
```

### Install the script into the user executable directory

```bash
install -Dm755 cli/pdfmanuc "$HOME/.local/bin/pdfmanuc"
```

Make sure `$HOME/.local/bin` is present in your `PATH`.

### Install the script into the system executable directory

```bash
sudo install -Dm755 cli/pdfmanuc /usr/local/bin/pdfmanuc
```

## Quick start

Compress a PDF file in place; the compressed file is created next to the
original one and the original is kept untouched:

```bash
pdfmanuc core.pdf
```

This produces `core.manuc.pdf` in the same directory as `core.pdf`.

## Advanced usage

```
pdfmanuc [options] <input.pdf>
```

| Option | Description |
|---|---|
| `-h`, `--help` | Show usage help and exit |
| `-o <file>` | Output file (default: `<input>.manuc.pdf` next to the input) |
| `-r <resolution>` | Target image resolution in DPI (default: `300`) |

Show the help:

```bash
pdfmanuc -h
```

Write the result to a specific file:

```bash
pdfmanuc -o out.pdf core.pdf
```

Use a custom resolution:

```bash
pdfmanuc -r 600 core.pdf
```

Combine options:

```bash
pdfmanuc -r 600 -o out.pdf core.pdf
```
