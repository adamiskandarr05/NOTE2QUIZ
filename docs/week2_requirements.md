# Requirements specification for note2quiz

Version: 1.1 | Updated: 9 November 2026

## Section 0 Project framing and application scope

### Problem and evidence

Students need practice questions, but writing clear questions and useful answer options takes time. Students also need to answer a self-test before seeing its key. Teachers need to inspect that key when preparing questions.

Steuer et al. discuss the time and cost of writing textbook self-test questions. Kurdi et al. describe the training and resources needed for question writing. See [Steuer et al. (2021)](https://arxiv.org/abs/2110.04123) and [Kurdi et al. (2020)](https://doi.org/10.1007/s40593-019-00186-y).

### Existing approaches

- [Quizlet Practice Tests](https://help.quizlet.com/hc/en-us/articles/25946589648013-Studying-with-Practice-Tests) creates questions from notes. This project will record how questions are generated, checked and reviewed.
- [Steuer et al. (2021)](https://arxiv.org/abs/2110.04123) selects textbook content and writes questions. This project also needs answer-option checks and separate student and teacher screens.
- [SciQ](https://aclanthology.org/W17-4413/) supplies science questions with supporting passages. It is a fixed dataset rather than a generator for selected course notes.
- [NotebookLM source discovery](https://blog.google/innovation-and-ai/models-and-research/google-labs/notebooklm-discover-sources/) recommends related web sources. note2quiz will begin with a selected list of public reading links.

### Engineering gap

The project needs to connect passage selection, question generation, source checks and saved results. Students should answer before seeing the key. Teachers should be able to inspect and correct drafts. Optional reading should help users revisit a topic. 

### Objectives

- **O1:** Design a way to find relevant passages in the selected course notes and keep their file names and page numbers.
- **O2:** Develop student quizzes and teacher review, with question checks, saved marks and optional related reading.
- **O3:** Evaluate question quality, source support, account access, privacy, saved marks, reading relevance, time and cost.

### Application scope

| Item | Scope |
|---|---|
| Intended users | Undergraduate students revising course material and teachers or tutors preparing practice questions. |
| Supported tasks | Choose a role; create a local account or sign in; add and choose notes; select a topic and 1 to 5 questions; practise or review according to role; see saved marks; optionally open related reading. |
| Knowledge domain | General course material. Public computing and business PDFs are initial test samples, not a subject restriction. |
| Operating context | A browser app running on one computer. Each account has its own workspace. Selected passages are sent to an external question writer only after permission. |
| Student flow | Create a set or choose an existing set; answer eligible questions with the key hidden; submit; view marks, explanations and supporting passages. Teacher acceptance is not required for a student's own self-test. |
| Teacher flow | Inspect the draft key and evidence; accept, edit or reject questions; practise with accepted questions. Editing an accepted question returns it to Draft. |
| Optional reading | A button after set creation and quiz completion. It matches topics against a selected public reading list. After a quiz, incorrect answers determine the focus; a perfect score uses the full quiz topic. |
| Input limits | English PDFs with selectable text; at most 3 files per request; at most 10 MB and 300 pages per file. |
| Constraints | One-semester project, limited service budget, permitted documents and local accounts. Roles are self-selected for local use. Basic checks do not prove that an answer is correct. |
| Outside scope | Classroom sharing, verified school identities, official grading, scanned-image reading, questions requiring diagrams, full mathematical proofs, running code, exam prediction, confidential exam papers and automatic web-page import. |
| Evaluation focus | Correctness, clarity and source support; hidden answers; teacher decisions; account isolation; saved marks; reading relevance; time and cost. |

## Section 1 Functional requirements

| ID | Requirement | Scope boundary |
|---|---|---|
| FR1 | The system shall let the user add and select course PDFs within the stated limits, choose a topic and receive a clear message for unsupported files. | It shall not silently use other course files or claim to read an image-only PDF. |
| FR2 | The system shall create the requested 1 to 5 draft questions from the selected topic and notes, with four distinct options, one marked answer and an explanation. | It shall not fill missing course information with unsupported facts. |
| FR3 | The system shall retain a real source file, PDF page and supporting passage for each answer. Teachers shall see this evidence during review; students shall see answer-specific evidence after submission. | It shall not invent page references or expose student answer keys through a preview response. |
| FR4 | The system shall let teachers inspect checks, accept, edit or reject questions, and save decisions and comments. Editing an accepted question shall return it to Draft. | Student accounts shall not use teacher review actions. Automated checks shall not record human acceptance. |
| FR5 | Student self-tests shall use non-rejected questions that pass the basic format and source checks. Teacher practice shall use accepted questions. The system shall hide student keys and explanations until submission, then score the quiz and show feedback. | Questions failing those checks shall not enter student quizzes. Draft or rejected questions shall not enter teacher practice. Marks shall not be presented as official grades. |
| FR6 | The system shall ask users to choose Student or Teacher before account creation or sign-in. Sign-in shall match the account's stored role, and the server shall enforce the role and workspace. | Choosing Teacher at sign-in shall not change a Student account into a Teacher account or expose another account's records. |
| FR7 | The system shall save each completed quiz's date, correct count, total, percentage, submitted answers and explanations, and show quiz history and the average score. | Refreshing, signing out or restarting shall not change completed marks. Editing a question later shall not rewrite a past quiz result. |
| FR8 | The system shall offer an optional Related notes button after set creation and quiz completion, showing up to three matching public links with titles, publishers and a short explanation. Unsupported topics shall receive a no-match message and an optional search link. | Recommendations shall not open automatically, change marks, add quiz sources automatically or claim to search the entire web. |

## Section 2 Non-functional requirements

These thresholds are proposed evaluation targets, not measured model results.

| ID | Quality | Requirement | Measurement method | Metric | Threshold |
|---|---|---|---|---|---|
| NFR1 | Speed | A five-question draft batch shall complete within the study time target. | Time six five-question requests from Generate to the displayed batch and checks, recording the connection and conditions. | 90th percentile batch time using nearest rank. | At most 45 seconds. |
| NFR2 | Correctness | Questions shall have a correct key and exactly one defensible option. | Two reviewers independently check 30 unedited generated questions against the notes, then resolve differences. | Final correct-question rate. | At least 90%, or 27/30. |
| NFR3 | Clarity | Question wording shall be understandable. | Rate the same 30 questions using the 0 to 2 clarity scale in the evaluation file. | Percentage with final clarity score 2. | At least 90%, or 27/30. |
| NFR4 | Cost | The evaluation writing cost shall remain within the student budget. | Record usage and test-date rates for all six requests, checks and retries, including equivalent charges covered by free credit. | Total service cost for 30 questions. | At most US$1.00. |
| NFR5 | Record reliability | Completed marks shall remain accurate and available in the correct account. | Compare saved results in six cases covering refresh, sign-in, account switching, restart and later question edits. | Lost or changed results; duplicate records. | 0 in all six cases. |

The 45-second target allows a short wait for five questions. The 90% correctness target is an initial goal for draft questions; errors still need review. The US$1.00 limit keeps the six-batch evaluation within a student budget.

## Section 3 Responsible AI requirements

| ID | Risk | Requirement | Measurement method | Metric | Threshold |
|---|---|---|---|---|---|
| RAI1 | Incorrect or unsupported answers | The system shall keep source references, block drafts with missing source quotes from student practice, disclose that generated questions can contain mistakes and show evidence after submission. Teachers shall be able to inspect evidence beforehand. | Check references and answer support for the 30 generated drafts. | Reference presence; answer-support rate. | 100% presence; at least 95% support, or 29/30. |
| RAI2 | Answer exposure or misuse of check results | The system shall hide student keys before submission, enforce each role's quiz rules and distinguish basic checks from teacher acceptance. | Run 20 workflow cases and 20 check cases containing 10 structural faults and 10 valid controls. | Early key exposures; ineligible questions admitted; faults flagged; false flags. | 0 exposures or blocked questions used; 10/10 structural faults flagged; at most 1/10 valid controls flagged. |
| RAI3 | Private information sent outside the app | The system shall obtain permission before sending selected passages and block labelled student names, student IDs and email addresses until removed. Scores, passwords and review comments shall not be sent to the question writer. | Run 20 cases using fake sensitive fields and inspect outgoing requests, including requests without permission. | Sensitive test values or excluded fields sent; requests without permission. | 0 in both measures. |
| RAI4 | Account or role misuse | The system shall require sign-in for workspace data, enforce the stored account role and keep notes and marks separate between accounts. | Run 12 cases covering missing sign-in, wrong roles, student review attempts, other-account access, sign-out and session expiry. | Unauthorised reads, changes or role upgrades. | 0 in all 12 cases. |
| RAI5 | Misleading reading suggestions | The system shall use real links from the selected public list, show publishers, allow users to skip suggestions and make no-match results clear. Reading suggestions shall not silently become quiz sources. | Review eight supported topics, two unsupported topics and four optional-button flows. | Relevant results; broken links; false matches; forced reading steps or source changes. | At least 7/8 supported topics receive a relevant result; 0 broken recommended links; 2/2 correct no-match responses; 0 forced steps or source changes. |

Privacy checks cover the defined fake fields, not every possible personal detail. Source-quote matching does not establish factual correctness or prove that only one option is correct.

### Reflection

RAI1 remains the hardest requirement to measure. A real passage can still fail to support the answer, and multiple options can seem reasonable. Students need answers hidden during practice and evidence they can check afterward. Two reviewers will rate correctness and clarity independently before resolving disagreements.
