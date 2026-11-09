# Evaluation criteria for note2quiz

Version: 1.1 | Updated: 9 November 2026

This is the plan for later testing. The 30-question quality evaluation and independent human ratings have not been completed.

## Test workload

- Generate 30 unedited questions in a teacher test account: 10 from Think Python Chapter 1, 10 from Teamwork in Business and 10 from The Foundations of Business. Use six requests of five questions, one document per request.
- Record topic, source pages, drafts, check flags, service version, settings, request time and usage. Use public text and exclude keys and passwords from saved evidence.
- Two reviewers familiar with the material rate the same 30 questions independently. Record percentage agreement before discussing differences and assigning final labels. Report results by source and subject.
- Run 20 workflow cases: 10 for student answer hiding, eligibility and submission, and 10 for teacher Draft, Accepted, Rejected and edited states. Separately run 20 structural-check cases: 10 faults and 10 valid controls.
- Run 20 privacy cases using fake details and 12 cases covering sign-in, roles and account access.
- Run six record cases: page refresh, sign-out and sign-in, server restart, switching accounts and returning, later question edits, and repeat submission. Compare the saved score, answers and record count.
- For reading, use eight supported topics, including Python, teamwork and mathematical functions, and two unsupported topics. Check the first three suggestions where available. Run four button flows: after set creation, after a quiz with incorrect answers, after a perfect quiz, and completing a quiz without opening suggestions.

PDF page numbers are one-based positions in the stored file, including its cover. Printed page numbers may differ. Source ranges and reading notes are in [data/README.md](../data/README.md).

## Criteria

| ID | Objective and requirement | Evaluation criterion | Capability bucket | Measurement method | Metric | Threshold | User outcome |
|---|---|---|---|---|---|---|---|
| E1 | O2, O3 / FR2 / NFR2 | Correct key and exactly one correct option | Domain-specific capability | Two reviewers compare 30 unedited drafts with the selected notes. | Final correct-question rate. | At least 90%, or 27/30. | Fewer misleading practice questions. |
| E2 | O1, O3 / FR1, FR3 / RAI1 | References use the selected file and support the answer | Instruction-following capability | Check the chosen file, open each cited page and inspect its passage. | Reference presence; wrong-source count; answer-support rate. | 100% presence; 0 wrong sources; at least 95% support, or 29/30. | Users can check an answer against the notes they selected. |
| E3 | O2, O3 / NFR3 | Clear question wording | Generation capability | Rate the same 30 drafts using the clarity scale below. | Percentage with final clarity score 2. | At least 90%, or 27/30. | Students understand what each question asks. |
| E4 | O2, O3 / FR4, FR5 / RAI2 | Student and teacher quiz rules work | Instruction-following capability | Run the 20 workflow cases and 20 structural-check cases. Check both the interface and server responses. | Early answer exposures; blocked questions used; faults found; valid controls flagged. | 0 exposures or blocked questions used; 10/10 faults found; at most 1/10 false flags. | Students answer first; teachers retain review control. |
| E5 | O2, O3 / RAI3 | Permission and outgoing-data controls work | Instruction-following capability | Inspect outgoing requests in 20 cases using fake sensitive fields. | Excluded values sent; requests without permission. | 0 in both measures. | Less unwanted sharing of private information. |
| E6 | O3 / NFR1, NFR4 | Time and service cost are acceptable | Cost and latency | Time and record usage for the six five-question requests, including checks and retries. | p90 batch time; total service cost. | At most 45 seconds; at most US$1.00. | A short study session remains practical. |
| E7 | O2, O3 / FR6 / RAI4 | Sign-in, roles and accounts are separated | Instruction-following capability | Run the 12 account cases, including direct server requests. Choosing Teacher must not upgrade an existing Student account. | Unauthorised reads, changes or role upgrades. | 0 across all 12 cases. | Users see the correct workspace and permitted tools. |
| E8 | O2, O3 / FR7 / NFR5 | Marks and submitted answers are retained correctly | Instruction-following capability | Compare stored results before and after the six record cases; recalculate the average from completed quizzes. | Lost or changed results; duplicate records; incorrect averages. | 0 across all six cases. | Students can trust their saved practice history. |
| E9 | O2, O3 / FR8 / RAI5 | Reading suggestions are useful and optional | Domain-specific capability | Review eight supported topics, two unsupported topics and four button flows. Open recommended links and judge course-topic relevance. | Supported topics with a relevant top-three result; broken links; correct no-match responses; forced steps or source changes. | At least 7/8 relevant; 0 broken links; 2/2 correct no-match responses; 0 forced steps or source changes. | Users can choose further reading without interrupting a quiz. |

## Rating and counting rules

**Correctness:** pass only when the key is correct, exactly one option is defensible and the explanation agrees with the notes. Rate the unedited draft, even if a teacher can later repair it.

**Source support:** pass only when the file and page exist, the quoted passage appears there and it supports the marked answer. A matching topic or word alone does not show that the answer is supported.

**Clarity:** 0 = unclear or misleading; 1 = understandable but needs editing; 2 = clear and understandable without editing. Judge wording separately from correctness.

**Quiz eligibility:** student self-tests may use Draft or Accepted questions when the basic format and source checks pass. Teacher practice uses Accepted questions only. Rejected questions are excluded from both. Editing returns an accepted question to Draft. Basic checks never count as teacher acceptance.

**Hidden answers:** inspect the student screen and server responses before submission for answer keys, explanations and answer-specific source quotes. Teachers may see this information during review. Student feedback should appear after submission.

**Known structural faults:** include incomplete or repeated options, invalid answer labels and missing or unmatched source fields. Human reviewers assess meaning-based ambiguity; a wording warning is not proof of an error.

**Reading relevance:** two reviewers judge whether at least one of the top three links offers useful reading on each supported topic. Record agreement before resolving differences. Unsupported topics pass only when no unrelated resource is recommended. A perfect quiz may receive broader reading rather than an incorrect-answer focus. The reading list has limited coverage.

**Time:** sort the six end-to-end times and take rank ceil(0.90 × 6). Record the small sample size and all failures; do not discard slow requests.

**Cost:** use service rates from the test date and include writing, checking and retry usage. Report actual cost and whether the budget was met.

## Reflection

Answer correctness is the main quality criterion. The role checks are also essential: requiring students to inspect the key before a self-test would defeat the intended flow. Saved marks and optional reading support revision, but neither demonstrates that the generated questions are correct.
