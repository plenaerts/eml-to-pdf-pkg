# eml_to_pdf

Convert `.eml` (email) files to PDF using only Python.

The converted PDF files will be saved in the specified output directory.
The output filenames are formatted as:
`YYYY-MM-DD_original_filename.pdf`, where:

- The date prefix is taken from the email's sent date
- Spaces in the original filename are converted to underscores
- The extension is changed to `.pdf`

For example, `My Email.eml` sent on March 15, 2024 will become
`2024-03-15_My_Email.pdf`.

## Features

- Converts email body (both plain text and HTML)
- Preserves email metadata (From, To, Subject, Date)
- Supports embedded images
- Lists email attachments in the PDF
- Supports various character encodings
- Maintains basic text formatting

## Purpose

This tool allows you to convert email files (`.eml` format) into PDF documents,
making them easier to archive, share, and view without requiring an email
client.

Based on various libraries but NOT on a full rendering engine like WebKit
or Gecko. [python-pdfkit and wkhtmltopdf are deprecated libraries](
    https://github.com/JazzCore/python-pdfkit?tab=readme-ov-file#deprecation-warning)

## Dependencies

- Python 3.9+
- [weasyprint](https://weasyprint.org/) - a visual rendering engine for HTML
and CSS that can export to PDF.
- [python-markdown](https://github.com/Python-Markdown/markdown) - for
  HTML'izing plain text.

## Installation

Clone or download this repo and use pip to install this package:

```bash
pip install .
```

Users of Arch linux or derived distro's like Manjora can use AUR package
[eml_to_pdf](https://aur.archlinux.org/packages/eml_to_pdf-git).

## Usage

```text
usage: eml_to_pdf [-h] [-d] [-p size] input_dir output_dir

Convert EML files to PDF

positional arguments:
  input_dir             Directory containing EML files
  output_dir            Directory for PDF output

options:
  -h, --help            show this help message and exit
  -d, --debug_html      Write intermediate html file next to pdf's
  -p size, --page size  a3 a4 a5 b4 b5 letter legal or ledger with or
                        without 'landscape', for example: 'a4 landscape' or
                        'a3' including quotes. Defaults to 'a4' and 'landscape'.
```

Example below renders all .eml files in `./emails` to a4 landscape oriented pdf's
in `./pdf`:

```bash
python eml-to-pdf.py -p 'a4 landscape' ./emails ./pdfs
```

Input file: `Meeting Notes.eml` (sent 2024-03-20)
Output file: `2024-03-20_Meeting_Notes.pdf`

## Issues

We've tested eml_to_pdf with a couple of cases with embedded images, tables,
unicode or specific encodings. Refer to
[tests](/klokie/eml-to-pdf/tree/main/tests) for example emails.

Please open an issue ticket if you have a mail where conversion results are
not usable, describe what you think your message contains, the output you
expect and attach an eml file. We're not promising a solution, but we can
have a look.

Please cleanup any attachments you add of things you don't want to share with
the world.

## License

MIT
