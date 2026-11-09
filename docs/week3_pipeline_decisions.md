# Week 3 pipeline decisions

Project: note2quiz | Date: 9 November 2026 | Pathway A: PDF/Text

## Link to Week 2

This work expands the Read and organise notes and Find source passages parts of the [Week 2 architecture](week2_architecture_v1.png). It supports FR1, FR3 and RAI1. The prepared passages provide file and page evidence for E2 in the [evaluation plan](week2_evaluation_criteria.md). The later 30-question answer-support evaluation is still needed.

## Sources and selected pages

The input is Think Python PDF pages 23 to 30 and Teamwork in Business PDF pages 2 to 5. Two files from different subjects are enough for this first preparation check. Source identity, licences and inspection findings are in the [data inventory](week3_data_inventory.md).

## Part B comparison

Both methods used the same 12 pages and a 500-character maximum. Each page was split separately.

| Measurement | Fixed-size splitting | Paragraph-aware splitting |
|---|---|---|
| Prepared passages | 57 | 62 |
| Think Python passages | 37 | 39 |
| Teamwork passages | 20 | 23 |
| Smallest passage, characters | 63 | 60 |
| Largest passage, characters | 500 | 499 |
| Cuts inside words | 28 | 0 |

The [notebook](../notebooks/week3_pipeline.ipynb) produced these results in both the local and Colab runs. The boundary check counts a cut between letters or digits and a cut between a line-end hyphen and the rest of its word. It does not rate whether a passage makes sense on its own.

The first fixed-size split ends with `complex sy`, and the next passage starts with `stems`. The chosen method keeps `systems` together. It produced five more passages but avoided the 28 measured word cuts.

The chosen method tries a blank line first, then a line break, then a word space in the last half of the allowed range. It avoids cutting after a line-end hyphen. Neither extracted sample contained blank-line paragraph breaks, so the fallback rules did most of the work. This does not recover the original paragraph structure or guarantee a complete idea in every passage.

## Chosen preparation

- Remove seven known Think Python page-header lines and four Teamwork footer lines. Clean trailing spaces and line endings; keep internal line breaks and indentation.
- Keep other extraction problems visible. Do not guess repairs to broken words, raised reference numbers or figure layout.
- Use page-aware paragraph splitting with a 500-character maximum and no overlap. Retain source ID, filename, PDF page, source checksum and character positions for every passage.
- Save one JSONL file containing 62 passages: 39 from Think Python and 23 from Teamwork. Character positions refer to the cleaned page text.

Think Python changed from 16,561 to 16,339 characters after cleaning. Teamwork changed from 9,680 to 9,452. The checks confirm that splitting retains all non-whitespace characters from those cleaned pages.

Sentences and ideas can still cross passage or page boundaries. Code spacing and figure reading order also need review before generating questions. More detailed quality checks belong to Topic 4.

## Workflow choices

Batch processing suits this small set of PDF pages, which is processed together rather than as a live stream. The prepared export follows ETL: extract PDF text, transform it, then load it into the prepared JSONL file. Original PDFs are retained separately so the preparation can be repeated.

Part B writes `data/processed/prepared_text.jsonl` and `data/week3_manifest.json`. Part C reruns the same preparation and writes `data/pipeline_v1/documents/prepared_text.jsonl` and `pipeline_manifest.json`. The manifests retain source versions, licences, source and output checksums, configuration and source-to-output links.

## Stage contracts

| Stage | Check and recorded evidence | Failure response |
|---|---|---|
| Ingest | Two permitted PDFs exist, meet the size limit and match the recorded source checksums. | Stop for missing, changed or unsupported input. |
| Inspect | Page ranges are valid and all 12 selected pages contain readable text. Show counts and samples. | Stop for an invalid range or unreadable page. |
| Prepare | Apply the chosen cleaning and splitting rules, with a file and PDF page for every passage. | Stop for empty text or invalid settings. |
| Validate | Reopen JSONL; check unique IDs, text, source, page, size and character coverage. | Stop if the saved records differ or required information is missing. |
| Record lineage | Save both source-to-output links, rights, settings and checksums. | Report missing metadata or a checksum mismatch. |

## Run evidence

The local pipeline ran twice. Both runs produced 62 records and a 44,580-byte prepared file with the same SHA-256 checksum. Part B and Part C prepared files also matched. The run manifest records PASS for matching sources, outputs, counts and mappings. Run timestamps are allowed to differ.

Two controlled failure checks passed: a missing source was stopped before reading, and empty text was stopped before preparation. The [diagram](week3_pipeline_diagram.png) shows these failures and responses.

The saved notebook also passed in Google Colab with Python 3.13.18 and pypdf 6.21.4. Its two runs produced the same prepared-file checksum as the local exports. The published manifests retain the earlier local run details. Matching files do not prove that the text is suitable for every future question.
