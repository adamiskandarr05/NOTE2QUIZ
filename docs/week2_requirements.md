# Requirements specification for note2quiz

Version: 1.0

## Section 0 Project framing and application scope

### Problem and evidence

Students need practice questions, but writing clear questions and good answer options takes time. note2quiz will create drafts from chosen notes and help a person check them before quiz use.

Steuer et al. discuss the time and cost of writing textbook self-test questions. Kurdi et al. explain the training and resources needed for manual question writing. See [Steuer et al. (2021)](https://arxiv.org/abs/2110.04123) and [Kurdi et al. (2020)](https://doi.org/10.1007/s40593-019-00186-y).

### Existing approaches

- [Quizlet Practice Tests](https://help.quizlet.com/hc/en-us/articles/25946589648013-Studying-with-Practice-Tests) creates questions from notes. Using its finished service would not provide our own recorded writing and checking process.
- [Steuer et al. (2021)](https://arxiv.org/abs/2110.04123) selects textbook content and writes questions. This project still needs a four-option checker and a review screen.
- [SciQ](https://aclanthology.org/W17-4413/) supplies science questions with supporting passages. It is a fixed dataset and does not create questions from chosen course notes.

### Engineering gap

The project needs one inspectable process for finding notes, writing questions, checking sources and options, and saving a human review decision. Its value will be tested; no claim of a new research method or better performance is made.

### Objectives

- **O1:** Design a way to find relevant passages in the selected course notes and keep their file names and page numbers.
- **O2:** Develop question writing, question checks, human review and a quiz made from accepted questions.
- **O3:** Evaluate question quality, source support, review controls, time and cost using a defined test set.

### Application scope

| Item | Scope |
|---|---|
| Intended users | Undergraduate students and tutors. The person reviewing a question may be its student author or a tutor. |
| Supported tasks | Add and choose course notes; select a topic and 1-5 questions; read drafts and evidence; accept, edit or reject drafts; take a quiz; see scores, explanations and sources. |
| Knowledge domain | General course learning material. Public computing and business documents are the initial test samples, not a subject restriction. |
| Operating context | A browser application for individual study. Selected passages are sent to an external question-writing service only after permission. |
| Input limits | English PDFs with selectable text, at most 3 files per request, 10 MB and 300 pages per file. |
| Constraints | One-semester student project, limited service budget, public or permitted documents, and human review before quiz use. |
| Outside scope | Scanned-image reading, questions requiring diagrams, full mathematical proofs, running code, official grading, predicting exam questions, personal advice and use of confidential exam papers. |
| Evaluation focus | Are questions correct, clear and supported by the chosen notes? Do checks and review controls catch problems? Are time and cost acceptable? |

## Section 1 Functional requirements

| ID | Requirement | Scope boundary |
|---|---|---|
| FR1 | The system shall let the user add and choose course PDFs within the stated limits and select a topic. It shall report unreadable or unsupported files. | The system shall not silently use another course's files or claim to read an image-only PDF. |
| FR2 | The system shall create the requested 1-5 draft questions from the selected topic and notes, each with four distinct options, one marked answer and a short explanation. | It shall not fill gaps using unsupported course facts. |
| FR3 | The system shall show the source file name, PDF page number and supporting passage for each draft answer, and report when the notes do not provide enough information. | It shall not invent page numbers or present missing evidence as confirmed support. |
| FR4 | The system shall show draft check results and let the reviewer accept, edit or reject a question, saving the decision and comments. Editing an accepted question shall return it to Draft. | Automated checks shall not mark a question as human accepted. |
| FR5 | The system shall build quizzes from accepted questions, hide answers until submission, calculate the score and then show explanations and sources. | Draft and rejected questions shall not appear in a quiz. Scores shall not be presented as official grades. |

## Section 2 Non-functional requirements

These thresholds are proposed targets for later testing, not measured results.

| ID | Quality | Requirement | Measurement method | Metric | Threshold |
|---|---|---|---|---|---|
| NFR1 | Speed | The system shall return a five-question draft batch within the study time target. | Time six requests, each for five questions, from Generate to displayed drafts and checks. Use the same connection and record conditions. | 90th percentile batch time, using the nearest-rank method. | At most 45 seconds. |
| NFR2 | Correctness | The system shall produce draft questions with a correct answer and exactly one defensible option. | Two reviewers check 30 unedited drafts against their source notes. Resolve differences after recording independent ratings. | Percentage with a correct key and only one correct option. | At least 80%, or 24 of 30. |
| NFR3 | Clarity | The system shall use wording students can understand. | Review the same 30 drafts using the clarity scale in the evaluation file. | Percentage receiving the final clarity score of 2. | At least 90%, or 27 of 30. |
| NFR4 | Cost | The system shall keep the evaluation writing cost within the student budget. | Record actual service usage and rates for the six five-question requests, including automated checks and retries. Count the equivalent charge even if free credit is used. | Total service cost in US dollars for the 30-question workload. | At most US$1.00. |

The 45-second target allows a short wait for five questions. The 80% draft target is an initial target because every question still needs review. The clarity target is higher because the project is for student practice. US$1.00 is the proposed test budget, not a price estimate.

## Section 3 Responsible AI requirements

| ID | Risk | Requirement | Measurement method | Metric | Threshold |
|---|---|---|---|---|---|
| RAI1 | Wrong or unsupported answers | The system shall show a real file, page and passage for each draft and keep unsupported drafts out of the accepted set until corrected and reviewed. | Inspect all 30 drafts and compare each reference and passage with the PDF. | Reference presence; percentage of passages that support the marked answer. | 100% reference presence; at least 95% support, or 29 of 30. |
| RAI2 | Unchecked questions being trusted | The system shall require explicit human acceptance before quiz use and show checks for missing fields, repeated options and possible ambiguity. | Run 20 review-state cases. Separately test 10 known structural faults and 10 valid controls. | Unapproved questions admitted; known faults flagged; valid controls wrongly flagged. | 0 unapproved; at least 9 of 10 faults flagged; at most 1 of 10 valid controls wrongly flagged. |
| RAI3 | Private information sent outside the application | The system shall obtain permission before sending passages and block selected text containing labelled student names, student IDs or email addresses until removed. It shall not send quiz scores or reviewer comments to the question writer. | Use 20 cases with fake sensitive fields and inspect outgoing requests; include requests made without permission. | Sensitive test values, scores or review comments sent; requests sent without permission. | 0 test values or excluded fields sent; 0 requests without permission. |

Privacy tests cover the defined fake fields. They do not prove that every possible personal detail will be detected. Only permitted, non-confidential notes are in scope.

### Reflection

RAI1 will be the hardest to measure. A real page reference can still fail to support an answer, and two options can appear reasonable. Two reviewers will compare the full question with the passage and record disagreements before reaching a final decision.
