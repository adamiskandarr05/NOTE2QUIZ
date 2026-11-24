# Data Quality, Bias, and Responsible Data Report - note2quiz

This report checks 62 passages from Topic 3: 39 from *Think Python* and 23 from *Teamwork in Business*. They came from 12 selected PDF pages. It does not cover every page, the third PDF, lecture notes, or generated questions. The [notebook](../notebooks/week4_quality.ipynb) shows the checks and outputs.

| Topic 2 requirement | Data needed | Quality concern | Check and decision |
|---|---|---|---|
| FR1: Read course PDFs | Readable text from selected pages | Completeness and accuracy | Compare sample text with the visible PDF; use or hold. |
| FR3 and RAI1: Show evidence for an answer | File name, PDF page and text position | Consistency and accuracy | Check the source hash, page and saved text position; use, repair or hold. |

## 1. Data Quality Scorecard

The ratings apply only to this selected sample. N.V. means not verified.

| Dimension | Rating (1–5 / N.V.) | Evidence | Action / limitation |
|---|---:|---|---|
| Completeness | 2/5 | All 62 records have text and source fields. Three passages are under 100 characters, two mention a figure, and some sentences are split between passages. | Check surrounding text and figures before making questions. |
| Consistency | 4/5 | All 62 source hashes, PDF page numbers and saved text positions match the extracted PDF text. Printed page numbers can differ from PDF page numbers. | Keep the file name and PDF page with each passage. |
| Accuracy | 2/5 | Manual reading found joined words on six of the eight first Python page passages. For example, the extraction says `isproblem` on PDF page 23 and `thatprintis` on page 25, while the visible PDF has spaces. | Hold the 39 Python passages until they are extracted again and checked. |
| Timeliness | N.V. | The books are from 2015 and 2023. The current version used by a future course is unknown. | Confirm the course topics and version before using them. |
| Uniqueness | 5/5 | No repeated IDs or exact text matches after making spaces and letter case consistent. | Repeat the check when more files are added. |

## 2. Validation and Data-Defect Findings

The manual check covered 16 passages: the first passage from each of the 12 pages, plus four unusual examples. The visible Python PDF was also checked on pages 23 and 25. Pandera checked the rules below. All 62 records passed these rules, but some text is still wrong.

| Rule | Failure it detects | Result | Action if it fails |
|---|---|---|---|
| Text present, valid ID, 1 to 500 characters | Empty or malformed passage | 0/62 (0%) | Hold and inspect the Topic 3 output. |
| Valid source, PDF page and source SHA-256 | Missing or changed source | 0/62 (0%) | Hold and check the PDF and manifest. |
| Text matches the saved part of the extracted PDF page | Wrong page or text position | 0/62 (0%) | Hold and extract the page again. |
| No NUL or replacement character | Obvious text corruption | 0/62 (0%) | Compare with the visible PDF. |

The check found three passages under 100 characters, two that mention a figure, and none with four spaces or four newlines in a row. Being under 100 characters is a warning about missing context, not proof that a passage is bad. The [review CSV](week4_validation_failures.csv) has 51 rows for 42 different records. It includes warnings and the 39 Python passages held because the same PDF has repeated text problems. These rows are **not** Pandera failures. No passage was proved to be outdated; the course version is still unknown.

| Case | Evidence checked | Decision and reason |
|---|---|---|
| `S01-p0023-c002`, joined words | The extracted text says `isproblem`; the visible PDF has separate words. | Hold Python passages for a better extraction. |
| `S01-p0027-c007`, short passage | It contains only the end of a definition on PDF page 27. | Hold until joined with the preceding text. |
| `S02-p0005-c004`, figure reference | It points to Figure 1.2 for percentage claims. | Hold until the figure can be checked. |
| `S02-p0003-c001`, figure reference | The caption is followed by readable text. | Keep the text; check any future question that needs the image. |

The joined words were found by reading. A text length or format rule did not catch them.

## 3. Duplicate and Anomaly Findings

The notebook compares text after making spaces and letter case consistent. It found **0 exact duplicates**. The [duplicate CSV](week4_duplicate_review.csv) has only its header. This check may miss questions that say the same thing in different words or use different versions. The original 62-record file stays unchanged.

All 39 Python passages are held because text errors appear on several sampled pages. This does **not** mean every Python passage is wrong. Two teamwork passages are also held: `S02-p0003-c007` is only part of a sentence, and `S02-p0005-c004` needs Figure 1.2. The [filtered file](../data/prepared_chunks_clean.jsonl) contains the other 21 teamwork passages. They are for checking only because not all were compared with the visible PDF. The matching [PKL file](../data/chunks_clean.pkl) has the same 21 records.

## 4. Representation, Coverage, and Bias Assessment

The [coverage chart](week4_coverage_by_source.png) shows the original 39 Python and 23 teamwork passages. After the hold, 0 Python and 21 teamwork passages remain for checking. These numbers cover selected pages only.

| Area needed | Expected evidence | Actual evidence | Gap |
|---|---|---|---|
| Basic computing questions | Clear passages from *Think Python* | 39 prepared, all held | Yes, until extraction is repaired. |
| Teamwork questions | Clear passages from *Teamwork in Business* | 21 passages for checking | Other pages and figures are not checked. |
| Wider business questions | Passages from *The Foundations of Business* | PDF collected, no prepared passages | Yes, if wider business topics are tested. |

| Risk | Source or preparation | Prepared passages | Possible effect on a question | Action and test |
|---|---|---|---|---|
| Historical | The 2015 Python book includes Python 2 examples. | A passage may lose its version label. | Search may return the example; a question may make old syntax look current. | Keep the label, confirm course version and review generated questions. |
| Representation | Only selected pages from two books were prepared. | Some topics have no passages. | Search may choose weak evidence, so a question may lack support. | Add the third PDF and check questions by topic. |
| Measurement | PDF extraction joins words and misses figures. | Some passages have wrong text or missing visual context. | Search may select them; bad text may appear in an answer. | Re-extract, inspect visible pages and check answers against sources. |

These are possible data risks. The final app has not been tested for differences between users or topics.

## 5. Privacy, Consent, Rights/Access, and Data Governance

The [Week 3 inventory](week3_data_inventory.md) and [manifest](../data/week3_manifest.json) record source names, versions, page ranges and file hashes. *Think Python* states CC BY-NC 3.0. *Teamwork in Business* states CC BY-NC-SA 4.0 except where noted. The PDF sources and credits are kept. Rights for third-party figures still need checking before wider use.

| Check | Status and evidence | Action |
|---|---|---|
| Source and version | Recorded for this sample | Check any new or changed PDF. |
| Rights | Book licences known; figure exceptions need review | Check credits before using figures. |
| Personal data | No accounts, marks or private notes in these passages | Check future uploaded notes. |
| Consent | N/A for this public book sample | Get permission for private notes before processing. |
| Updates and removal | Course version not confirmed | Confirm it and replace old exports if needed. |

## 6. Mitigation Plan and Residual Risk

| Issue | Evidence | Action | Owner / timing | Residual risk |
|---|---|---|---|---|
| Python text | Joined words on six of eight sampled pages | Extract the text again, inspect pages and rerun checks. | Before making questions | Other text errors may remain. |
| Teamwork fragments and figures | Two held passages | Join the sentence or include and check the figure. | Before using those passages | Other pages may need figures. |
| Limited coverage | Selected pages from two PDFs | Prepare the third PDF and report results by source. | Before the 30-question trial | Three books still cover few subjects. |
| Old examples and rights | Python 2 text; licence exceptions | Confirm course version and check figure credits. | Before wider use | More old examples or third-party content may remain. |

## 7. Impact on Topic 2 Requirements / Evaluation Criteria

- **FR1:** The selected PDFs have readable extracted text, but the Python output needs repair. Scanned pages and figure-only information are not handled here.
- **FR3 and RAI1:** File, page and position checks show where text came from. They do not prove that a future correct answer is supported by it.
- **E2 and NFR2:** The 30-question trial must still check answer correctness and source support with human reviewers.
- **Privacy and cost:** This lab used no student data, model call or API key, so it did not measure these requirements.

## 8. Topic 4 Quality Gate Decision

**HOLD for question generation.** The automatic checks passed, but the Python text has repeated errors. Only selected teamwork pages remain in the filtered file. The next steps are to extract the Python text again, fix the two held teamwork passages, check the pages, and rerun the notebook. The 21-record file is for checking, not yet for making questions.
