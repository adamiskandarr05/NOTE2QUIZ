# Week 3 data inventory

Pathway A: PDF/Text

These computing and business PDFs support [FR1, FR3 and RAI1](week2_requirements.md): reading course PDFs, keeping source files and pages, and checking source evidence.

## Sources and inspection

| Source | Filename and purpose | Version and owner | Access and rights | Observed inspection evidence |
|---|---|---|---|---|
| S01 | [think_python_2e.pdf](../data/think_python_2e.pdf). Introductory programming text. | Second edition, version 2.4.1; copyright 2015. Allen B. Downey, Green Tea Press. | Public PDF. CC BY-NC 3.0; licence on PDF page 4. | 907,689 bytes; 244 PDF pages. Selected pages 23 to 30 contain 16,561 extracted characters; no selected page is empty. |
| S02 | [teamwork_in_business.pdf](../data/teamwork_in_business.pdf). Teamwork example and team characteristics. | Fundamentals of Business, fourth edition, 2023. Adapted by Ron Poff, Virginia Tech. | Public PDF. CC BY-NC-SA 4.0, except where noted; licence on PDF page 1. | 1,424,558 bytes; 20 PDF pages. Selected pages 2 to 5 contain 9,680 extracted characters; no selected page is empty. |

The notebook shows extracted samples from S01 page 23 and S02 page 2. The selected ranges cover 12 pages.

Original sources: [Think Python](https://greenteapress.com/thinkpython2/thinkpython2.pdf) and [Teamwork in Business](https://vtechworks.lib.vt.edu/bitstreams/38bd0a78-433e-4d0e-aa83-e0e0ff9b9b82/download). The notebook checks the source checksums against a fixed repository version recorded in [the Part B manifest](../data/week3_manifest.json).

## What the inspection showed

- Think Python includes code, line-end hyphens and joined words such as `isproblem`. The code keeps internal spacing and line breaks rather than guessing repairs.
- Teamwork in Business includes repeated footers, captions and raised reference numbers. Removing the known footer does not fix reading order around figures.
- Neither selected source produced blank-line paragraph breaks. The paragraph-aware splitter therefore mainly uses line and word breaks.
- PDF positions differ from printed page numbers. Every prepared passage keeps the one-based PDF position.

## Storage and rights

Original repository files remain in `data/` and are unchanged. The notebook copies the two selected files to temporary `data/raw/` inside its workspace. Part B saves [prepared text](../data/processed/prepared_text.jsonl) and [its manifest](../data/week3_manifest.json). Part C saves [prepared text](../data/pipeline_v1/documents/prepared_text.jsonl) and [its run manifest](../data/pipeline_v1/documents/pipeline_manifest.json).

Prepared passages keep their source licences and attribution. See [the source credits](../data/README.md) for licence links and exceptions. These files are used for a non-commercial course project.

## Execution status

All 11 code cells passed in Colab and produced 62 passages. The prepared-file checksum matches the earlier local run. The notebook saves the Colab results; the manifests record the earlier local run.
