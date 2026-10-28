# Evaluation criteria for note2quiz

Version: 1.0

All checks below are planned. No model test results or user ratings have been collected yet.

## Test workload

- Create 30 unedited draft questions: 10 from Think Python Chapter 1, 10 from Teamwork in Business and 10 from The Foundations of Business.
- Use six requests of five questions. Choose one source document for each request so source selection can be checked. Two requests are used for each document.
- Record the selected topic, source pages, draft, check flags, service version, request settings, time and usage. Use public test text only.
- Two reviewers familiar with the material rate each question independently. Record percentage agreement before discussing differences to produce final labels. Show results by source and subject as well as overall.
- Use 20 separate workflow cases for Draft, Accepted, Rejected and edited questions; 20 separate check cases with 10 known structural faults and 10 valid controls; and 20 privacy cases using fake personal details. These are planned test cases, not collected results.

PDF page numbers mean the one-based page position in the stored file, including its cover. Printed book page numbers may differ. Initial source ranges and reading notes are in [data/README.md](../data/README.md).

## Criteria

| ID | Objective and requirement | Evaluation criterion | Capability bucket | Measurement method | Metric | Threshold | User outcome |
|---|---|---|---|---|---|---|---|
| E1 | O2, O3 / FR2 / NFR2 | Correct answer and one correct option | Domain-specific capability | Compare 30 unedited drafts with the notes using two reviewers. | Final correct-question rate. | At least 80%, or 24/30. | Students spend less time fixing wrong draft questions. |
| E2 | O1, O3 / FR3 / RAI1 | References are present and support the answer | Instruction-following capability | Open each cited page and inspect its quoted passage. | Reference presence rate; answer-support rate. | 100% presence; at least 95% support, or 29/30. | Students can check an answer against the notes. |
| E3 | O2, O3 / NFR3 | Clear question wording | Generation capability | Rate the same 30 drafts on the 0-2 clarity scale below. | Percentage with final score 2. | At least 90%, or 27/30. | Students can understand what each question asks. |
| E4 | O2, O3 / FR4, FR5 / RAI2 | Review states and draft checks work | Instruction-following capability | Run 20 state cases and the 20 structural-check cases. | Unapproved items admitted; fault-detection rate; false-flag rate on valid controls. | 0 unapproved; at least 9/10 faults found; at most 1/10 valid controls flagged. | Unreviewed or clearly broken drafts stay out of the quiz. |
| E5 | O2, O3 / RAI3 | Permission and privacy controls work | Instruction-following capability | Run 20 cases with fake details and inspect outgoing requests. | Sensitive test values or excluded fields sent; requests without permission. | 0 in both measures. | Reduces unwanted sharing of private information. |
| E6 | O3 / NFR1, NFR4 | Time and service cost are acceptable | Cost and latency | Time and record usage for the six five-question requests, including check calls and retries. | p90 batch time; total service cost. | At most 45 seconds; at most US$1.00. | A short study session stays practical and affordable. |

## Rating rules

**Correctness:** pass only when the key is correct, exactly one option is defensible and the explanation agrees with the chosen notes. Otherwise fail.

**Source support:** pass only when the file and PDF page exist, the passage appears there and it supports the marked answer. A matching topic or keyword alone is not enough.

**Clarity scale:** 0 = unclear or misleading; 1 = understandable but needs editing; 2 = clear, specific and understandable without editing. Judge wording separately from factual correctness.

**Known structural faults:** include missing options, repeated options, a missing or invalid answer label, and missing source fields. Possible meaning-based ambiguity is also recorded during the 30-question review, but an automated warning is not proof of an error.

**Time:** measure from Generate to the complete displayed batch and its check results. Sort the six times and take rank ceil(0.90 x 6). Report the small sample size and any failures; do not silently discard slow or failed requests.

**Cost:** include all writing, checking and retry calls for the workload. Record the service's rates on the test date. Report actual cost and whether the budget was met.

## Reflection

Answer correctness is the most important criterion. A fast and clear question is still harmful to learning if its key is wrong. Source support and review controls help users find and correct those errors before practising.
