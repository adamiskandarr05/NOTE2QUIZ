# note2quiz project scope

Version: 1.1 | Updated: 9 November 2026

## Project name

note2quiz

## Domain

Higher education and study support.

## Problem statement

Students need practice questions to check their understanding of course material. Writing clear questions with one correct answer and three useful wrong options takes time. note2quiz will turn selected course notes into draft questions and show the passages that support the answers.

Users choose Student or Teacher before creating a local account or signing in. Both roles choose a course, notes and topic. The system finds relevant passages, writes draft questions and checks their format and source quotes.

Students take a self-test with answer keys hidden until submission. Teachers can inspect, edit, accept or reject drafts; their practice quizzes use accepted questions. Basic checks are separate from teacher approval and do not prove an answer is correct.

The app saves marks, answers and past results in each account. An optional Related notes button suggests public reading after creating a set or finishing a quiz. After a quiz it focuses on questions answered incorrectly, or on the full quiz topic when every answer is correct. Opening these links is optional and does not change the quiz's selected sources.

The first version will generate questions from English PDFs with selectable text across different subjects.

## Evidence of the problem

1. Steuer et al. explain that writing self-assessment questions is time-consuming and expensive, which limits the questions available in many textbooks. Their study examines selecting useful textbook content and generating questions. [Steuer, T., Filighera, A., Meuser, T. and Rensing, C. (2021), I Do Not Understand What I Cannot Define: Automatic Question Generation With Pedagogically-Driven Content Selection, arXiv preprint](https://arxiv.org/abs/2110.04123).
2. Kurdi et al. describe question writing as work that needs training, experience and resources. Their review discusses limits in question variety, difficulty control, feedback and evaluation. [Kurdi, G., Leo, J., Parsia, B., Sattler, U. and Al-Emari, S. (2020), A Systematic Review of Automatic Question Generation for Educational Purposes, International Journal of Artificial Intelligence in Education, 30, 121-204](https://doi.org/10.1007/s40593-019-00186-y).

## Related work

| Study or tool | What it does | Limitation for this project |
|---|---|---|
| [Quizlet Practice Tests](https://help.quizlet.com/hc/en-us/articles/25946589648013-Studying-with-Practice-Tests) | Creates practice questions from uploaded notes or flashcard sets. | Using the finished service would not give this project its own recorded question-writing and checking process. |
| [Steuer et al. (2021)](https://arxiv.org/abs/2110.04123) | Selects textbook content and writes questions using teaching principles. | This project also checks answer options, supports teacher review and saves quiz marks. |
| [SciQ, Welbl, Liu and Gardner (2017)](https://aclanthology.org/W17-4413/) | Provides science multiple-choice questions and supporting passages. | It is a fixed question set, limited to science, rather than a generator for selected course notes. |
| [NotebookLM source discovery](https://blog.google/innovation-and-ai/models-and-research/google-labs/notebooklm-discover-sources/) | Finds related sources on the web. | note2quiz's first version uses a smaller selected reading list. Its reading suggestions can focus on questions answered incorrectly. |

## Engineering gap

The project needs to connect generated questions to source pages, teacher decisions and saved marks. Students need to answer before seeing the key; teachers need to see the key when preparing questions. Optional reading should help users revisit a topic. The checks still need evaluation because a real citation does not prove that an answer is correct.

## Objectives

- **O1:** Design a way to find relevant passages in the selected course notes and keep their file names and page numbers.
- **O2:** Develop student quizzes and teacher review, with question checks, saved marks and optional related reading.
- **O3:** Evaluate question quality, source support, account access, privacy, saved marks, reading relevance, time and cost.

## Target users

Undergraduate students revising course material and teachers or tutors preparing practice questions. Accounts and their records are local to one computer. Roles are selected by users; classroom sharing and school sign-in are outside this version.

## Data sources

1. Allen B. Downey, Think Python, second edition, version 2.4.1. [Public PDF](https://greenteapress.com/thinkpython2/thinkpython2.pdf). The initial test will use Chapter 1, PDF pages 23-30. Text licence: [CC BY-NC 3.0](https://creativecommons.org/licenses/by-nc/3.0/).
2. Ron Poff (2023), Fundamentals of Business, fourth edition, Chapter 1, Teamwork in Business. [Public PDF](https://vtechworks.lib.vt.edu/bitstreams/38bd0a78-433e-4d0e-aa83-e0e0ff9b9b82/download). Licence: CC BY-NC-SA 4.0, except where otherwise stated.
3. Ron Poff (2023), Fundamentals of Business, fourth edition, Chapter 2, The Foundations of Business. [Public PDF](https://vtechworks.lib.vt.edu/bitstreams/a72a10fa-9658-4452-b33d-af42eecacd98/download). Licence: CC BY-NC-SA 4.0, except where otherwise stated.

The business chapters come from the same book. Together with Think Python, they provide three test documents from two subjects. Other permitted course notes can be added. Copies, attribution and reading notes are in [data](../data/README.md).

Optional reading will use a separate list of public pages from the Python Software Foundation, MIT OpenCourseWare and OpenStax. It provides links to extra reading rather than adding web content to a quiz automatically. Unsupported topics show a no-match message and an optional web-search link.

## Similar to EduAdvisor

Both systems use selected documents, find relevant passages and show source references so users can check the output.

## Different from EduAdvisor

EduAdvisor answers academic advising questions. note2quiz creates practice questions from course notes, separates student practice from teacher review, saves quiz marks and offers optional reading links.

## Responsible AI risks

| Risk | Possible harm | Planned control |
|---|---|---|
| Wrong answer or weak supporting evidence | A student learns an incorrect fact. | Block drafts with missing source quotes, explain that generated questions can contain mistakes, and show the key and evidence after submission. Teachers can check drafts before use. |
| Two correct options or confusing wording | A student receives a misleading question. | Check for repeated or missing options; let teachers edit or reject questions; use human ratings to evaluate correctness and clarity. |
| Over-trusting a check result | A matching quote is mistaken for proof that the answer is correct. | Keep basic checks separate from teacher acceptance. Explain the limits of the checks in the student flow. |
| Answers shown before a self-test | The student already knows the marked option before answering. | Hide student answer keys and explanations until submission. Keep teacher review in a separate role. |
| Wrong course material is used | Practice questions cover the wrong course. | Search only the chosen course files and show the file name for every question. |
| Private information or restricted notes are shared | Personal information or protected material reaches another service. | Use permitted notes, check sensitive fields and ask permission before sending selected passages. Keep keys and private files out of GitHub. |
| Account records are exposed | One user sees another user's notes or marks. | Require sign-in, separate local workspaces and enforce the account role on the server. |
| Unrelated reading is suggested | A student spends time on material outside the course. | Use real links from the selected reading list, show the publisher, explain the match and allow users to skip it. |

## Why GitHub

GitHub will keep the project documents, code, prompts and later test results together. Its history will show what changed and why. The repository is [adamiskandarr05/NOTE2QUIZ](https://github.com/adamiskandarr05/NOTE2QUIZ).
