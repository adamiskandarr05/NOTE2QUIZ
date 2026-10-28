# note2quiz

Turns course notes into practice questions and shows the pages that support the answers.

## Problem statement

Students need practice questions to check what they understand. Writing clear questions, correct answers and useful wrong options takes time. note2quiz will use selected course notes to draft questions, show the supporting passages and let a person check each question before it is used in a quiz.

The project covers different subjects. The first version will work with English PDFs that contain selectable text. It is a planned student project; the application and its performance tests will be developed in later labs.

## Evidence of the problem

- Writing textbook self-test questions takes time and resources, which can limit their availability. [Steuer et al., 2021](https://arxiv.org/abs/2110.04123).
- Writing good questions requires training and experience. Question variety, feedback and evaluation remain important issues. [Kurdi et al., 2020](https://doi.org/10.1007/s40593-019-00186-y).

## Related work

- [Quizlet Practice Tests](https://help.quizlet.com/hc/en-us/articles/25946589648013-Studying-with-Practice-Tests) already creates questions from notes. Using its finished service would not provide this project with its own recorded question-writing and checking process.
- [Steuer et al., 2021](https://arxiv.org/abs/2110.04123) selects textbook content and writes questions. A four-option question checker and a review screen still need to be built for this project.
- [SciQ, Welbl et al., 2017](https://aclanthology.org/W17-4413/) provides science questions and supporting passages. It is a fixed question set and does not create questions from a student's chosen notes.

These are limits for the needs of this project, not claims that note2quiz is the first or best tool of its kind.

## Engineering gap

The project will connect question writing with page references, checks for missing or repeated options, possible ambiguity warnings and a saved review decision. The main task is to make this process easy to inspect and test.

## Objectives

- **O1:** Design a way to find relevant passages in the selected course notes and keep their file names and page numbers.
- **O2:** Develop question writing, question checks, human review and a quiz made from accepted questions.
- **O3:** Evaluate question quality, source support, review controls, time and cost using a defined test set.

## Target users

Undergraduate students revising their courses, and tutors who want to check draft practice questions.

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

## Weekly progress

| Week | Focus | Deliverable | Status |
|---|---|---|---|
| W1 | Project scope and repository setup | Scope, README, group observation sheet and system map | Complete |
| W2 | Requirements, evaluation and design | Requirements, evaluation criteria, architecture and decisions | Complete |

## Week 3 preparation

Three public PDFs and reading notes are in `data/`. Coding will start in later labs using [Google Colab](https://colab.research.google.com/). Sign in with your Google account before the Week 3 lab.
