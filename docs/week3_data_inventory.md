# Week 3 data inventory

Project: note2quiz | Date: 9 November 2026 | Pathway A: PDF/Text

## Why these files

FR1 needs readable course PDFs. FR3 needs the source file, PDF page and supporting passage. RAI1 needs evidence that can be checked later. These requirements are in [Week 2 requirements](week2_requirements.md). The files below provide computing and business examples from the existing project data.

## Sources and inspection

| Source | Filename and purpose | Version and owner | Access and rights | Observed inspection evidence |
|---|---|---|---|---|
| S01 | [think_python_2e.pdf](../data/think_python_2e.pdf). Introductory programming text. | Second edition, version 2.4.1; copyright 2015. Allen B. Downey, Green Tea Press. | Public PDF. CC BY-NC 3.0; licence on PDF page 4. | 907,689 bytes; 244 PDF pages. Selected pages 23 to 30 contain 16,561 extracted characters; no selected page is empty. |
| S02 | [teamwork_in_business.pdf](../data/teamwork_in_business.pdf). Teamwork example and team characteristics. | Fundamentals of Business, fourth edition, 2023. Adapted by Ron Poff, Virginia Tech. | Public PDF. CC BY-NC-SA 4.0, except where noted; licence on PDF page 1. | 1,424,558 bytes; 20 PDF pages. Selected pages 2 to 5 contain 9,680 extracted characters; no selected page is empty. |

The notebook prints extracted text samples from PDF page 23 of S01 and page 2 of S02. Together, the selected ranges cover 12 pages. The ranges were chosen to test the preparation method on a small sample.

Original sources: [Think Python](https://greenteapress.com/thinkpython2/thinkpython2.pdf) and [Teamwork in Business](https://vtechworks.lib.vt.edu/bitstreams/38bd0a78-433e-4d0e-aa83-e0e0ff9b9b82/download). Source copies are fixed to repository commit `7e898e9011d0a898d46c173ffb0fbea056d8c85f`. The notebook checks their SHA-256 checksums before reading them. Full checksums and source details are saved in [the Part B manifest](../data/week3_manifest.json).

## What the inspection showed

- Think Python includes code, line-end hyphens and joined words such as `isproblem`. The code keeps internal spacing and line breaks rather than guessing repairs.
- Teamwork in Business includes repeated footers, captions and raised reference numbers. Removing the known footer does not fix reading order around figures.
- Neither selected source produced blank-line paragraph breaks. The paragraph-aware splitter therefore mainly uses line and word breaks.
- PDF positions differ from printed page numbers. Every prepared passage keeps the one-based PDF position.

## Storage and rights

Original repository files remain in `data/` and are unchanged. The notebook copies the two selected files to temporary `data/raw/` inside its workspace. Part B saves [prepared text](../data/processed/prepared_text.jsonl) and [its manifest](../data/week3_manifest.json). Part C saves [prepared text](../data/pipeline_v1/documents/prepared_text.jsonl) and [its run manifest](../data/pipeline_v1/documents/pipeline_manifest.json).

Prepared text retains its source licence. S01 passages remain under [CC BY-NC 3.0](https://creativecommons.org/licenses/by-nc/3.0/); S02 passages remain under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), with the source's exceptions. Source IDs identify the correct attribution for each passage. This is a non-commercial course project. The exports contain selected public book text and no student records.

## Execution status

The notebook passed all 11 code cells in Google Colab using Python 3.13.18 and pypdf 6.21.4. It produced 62 passages and passed the repeatability and failure checks. Its prepared-file checksum matches the earlier local run. The saved notebook contains the Colab outputs; the manifests retain the earlier local Python 3.12.14 run details.
