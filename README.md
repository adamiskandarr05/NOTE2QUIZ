# note2quiz

Turns course notes into practice questions and shows the pages that support the answers.

## Problem statement

Students need practice questions to check what they understand. Writing clear questions, correct answers and useful wrong options takes time. note2quiz creates draft questions from selected course notes and keeps the passages that support the answers.

Students answer before seeing the key and supporting passage. Teachers can edit, accept or reject drafts. Basic format and source checks help find errors, but the questions still need review.

The planned features include separate Student and Teacher accounts, saved quiz marks and optional links to related reading.

The first version supports English PDFs with selectable text across different subjects. The 30-question quality evaluation is planned for later work.

## Evidence of the problem

- Writing textbook self-test questions takes time and resources, which can limit their availability. [Steuer et al., 2021](https://arxiv.org/abs/2110.04123).
- Writing good questions requires training and experience. Question variety, feedback and evaluation remain important issues. [Kurdi et al., 2020](https://doi.org/10.1007/s40593-019-00186-y).

## Related work

- [Quizlet Practice Tests](https://help.quizlet.com/hc/en-us/articles/25946589648013-Studying-with-Practice-Tests) already creates questions from notes. This project will build and test its own question-writing and review steps.
- [Steuer et al., 2021](https://arxiv.org/abs/2110.04123) selects textbook content and writes questions. This project also checks answer options, supports teacher review and saves quiz marks.
- [SciQ, Welbl et al., 2017](https://aclanthology.org/W17-4413/) provides science questions and supporting passages. It is a fixed question set and does not create questions from a student's chosen notes.
- [NotebookLM source discovery](https://blog.google/innovation-and-ai/models-and-research/google-labs/notebooklm-discover-sources/) recommends related web sources. note2quiz's first reading feature uses a selected list of public links and can focus on questions answered incorrectly.

## Engineering gap

The main task is to connect generated questions to their source pages and check them before use. Student practice and teacher review need separate screens so students can answer without seeing the key first.

## Objectives

- **O1:** Design a way to find relevant passages in the selected course notes and keep their file names and page numbers.
- **O2:** Develop student quizzes and teacher review, with question checks, saved marks and optional related reading.
- **O3:** Evaluate question quality, source support, account access, privacy, saved marks, reading relevance, time and cost.

## Target users

Undergraduate students revising their courses and teachers or tutors preparing practice questions.

## Data sources

- [Think Python, second edition](data/think_python_2e.pdf), Allen B. Downey. [Original PDF](https://greenteapress.com/thinkpython2/thinkpython2.pdf).
- [Teamwork in Business](data/teamwork_in_business.pdf), Chapter 1 of Fundamentals of Business, fourth edition, Ron Poff. [Original PDF](https://vtechworks.lib.vt.edu/bitstreams/38bd0a78-433e-4d0e-aa83-e0e0ff9b9b82/download).
- [The Foundations of Business](data/foundations_of_business.pdf), Chapter 2 of the same book. [Original PDF](https://vtechworks.lib.vt.edu/bitstreams/a72a10fa-9658-4452-b33d-af42eecacd98/download).

These are initial test documents. Other permitted course documents can be added. See [source details, licences and PDF reading notes](data/README.md).

## Lab documents

- [Week 1 project scope](docs/week1_project_scope.md)
- [Group observation sheet](docs/week1_observation_sheet.md)
- [Group system map](docs/week1_system_map.png)
- [Week 2 requirements](docs/week2_requirements.md)
- [Week 2 evaluation criteria](docs/week2_evaluation_criteria.md)
- [Week 2 architecture diagram](docs/week2_architecture_v1.png)
- [Week 2 architecture decisions and traceability](docs/week2_architecture_decisions.md)
- [Week 3 pipeline notebook](notebooks/week3_pipeline.ipynb)
- [Week 3 data inventory](docs/week3_data_inventory.md)
- [Week 3 pipeline diagram](docs/week3_pipeline_diagram.png)
- [Week 3 pipeline decisions](docs/week3_pipeline_decisions.md)

## Weekly progress

| Week | Focus | Deliverable | Status |
|---|---|---|---|
| W1 | Project scope and repository setup | Scope, README, group observation sheet and system map | Complete |
| W2 | Requirements, evaluation and design | Requirements, evaluation criteria, architecture and decisions | Complete |
| W3 | PDF data preparation | Notebook, inventory, diagram, decisions and prepared exports | Complete |

## Week 3 data pipeline

The notebook prepares 62 passages from 12 selected pages in two public PDFs. It keeps source files and PDF page numbers. The local and Google Colab runs produced matching prepared files. See the [Part B manifest](data/week3_manifest.json) and [Part C run manifest](data/pipeline_v1/documents/pipeline_manifest.json).

[Open the notebook in Google Colab](https://colab.research.google.com/github/adamiskandarr05/NOTE2QUIZ/blob/main/notebooks/week3_pipeline.ipynb) to rerun the steps. The saved notebook contains the completed Colab outputs. The manifests retain the earlier local run details; both runs produced the same prepared-file checksum. No model API key is needed.
