# note2quiz project scope

## Project name

note2quiz

## Domain

Higher education and study support.

## Problem statement

Students need practice questions to check their understanding of course material. Writing clear questions with one correct answer and three useful wrong options takes time. note2quiz will turn selected course notes into draft questions and show the passages that support the answers.

Users will choose a course, notes and topic. The system will find relevant passages, write questions, check the drafts and let a person accept, edit or reject them. Only accepted questions will be used in quizzes.

A question-writing service is needed to turn passages into new questions, answer choices and explanations. The first version will support English PDFs with selectable text across different subjects.

## Evidence of the problem

1. Steuer et al. explain that writing self-assessment questions is time-consuming and expensive, which limits the questions available in many textbooks. Their study examines selecting useful textbook content and generating questions. [Steuer, T., Filighera, A., Meuser, T. and Rensing, C. (2021), I Do Not Understand What I Cannot Define: Automatic Question Generation With Pedagogically-Driven Content Selection, arXiv preprint](https://arxiv.org/abs/2110.04123).
2. Kurdi et al. describe question writing as work that needs training, experience and resources. Their review discusses limits in question variety, difficulty control, feedback and evaluation. [Kurdi, G., Leo, J., Parsia, B., Sattler, U. and Al-Emari, S. (2020), A Systematic Review of Automatic Question Generation for Educational Purposes, International Journal of Artificial Intelligence in Education, 30, 121-204](https://doi.org/10.1007/s40593-019-00186-y).

## Related work

| Study or tool | What it does | Limitation for this project |
|---|---|---|
| [Quizlet Practice Tests](https://help.quizlet.com/hc/en-us/articles/25946589648013-Studying-with-Practice-Tests) | Creates practice questions from uploaded notes or flashcard sets. | Using the finished service would not give this project its own recorded question-writing and checking process. |
| [Steuer et al. (2021)](https://arxiv.org/abs/2110.04123) | Selects textbook content and writes questions using teaching principles. | A four-option question checker and a review screen still need to be built for this project. |
| [SciQ, Welbl, Liu and Gardner (2017)](https://aclanthology.org/W17-4413/) | Provides science multiple-choice questions and supporting passages. | It is a fixed question set, limited to science, rather than a generator for selected course notes. |

These are comparisons with this project's needs. They do not establish that note2quiz has unique features or better results.

## Engineering gap

The practical task is to join question writing, source pages, draft checks and saved reviewer decisions in a small application. Each draft should be easy to inspect before it becomes a practice question. The checks must also be tested because a real citation does not prove an answer is correct.

## Objectives

- **O1:** Design a way to find relevant passages in the selected course notes and keep their file names and page numbers.
- **O2:** Develop question writing, question checks, human review and a quiz made from accepted questions.
- **O3:** Evaluate question quality, source support, review controls, time and cost using a defined test set.

## Target users

Undergraduate students revising course material and tutors reviewing draft questions.

## Data sources

1. Allen B. Downey, Think Python, second edition, version 2.4.1. [Public PDF](https://greenteapress.com/thinkpython2/thinkpython2.pdf). The initial test will use Chapter 1, PDF pages 23-30. Text licence: [CC BY-NC 3.0](https://creativecommons.org/licenses/by-nc/3.0/).
2. Ron Poff (2023), Fundamentals of Business, fourth edition, Chapter 1, Teamwork in Business. [Public PDF](https://vtechworks.lib.vt.edu/bitstreams/38bd0a78-433e-4d0e-aa83-e0e0ff9b9b82/download). Licence: CC BY-NC-SA 4.0, except where otherwise stated.
3. Ron Poff (2023), Fundamentals of Business, fourth edition, Chapter 2, The Foundations of Business. [Public PDF](https://vtechworks.lib.vt.edu/bitstreams/a72a10fa-9658-4452-b33d-af42eecacd98/download). Licence: CC BY-NC-SA 4.0, except where otherwise stated.

The two business chapters have the same parent book. Together with Think Python, they provide three public documents from two subjects for the first tests. They do not limit the courses the system is designed to support. Copies, attribution and reading notes are in [data](../data/README.md).

## Similar to EduAdvisor

Both systems use selected documents, find relevant passages and show source references so users can check the output.

## Different from EduAdvisor

EduAdvisor answers academic advising questions. note2quiz creates practice questions from course notes. It must also check the answer options, save review decisions and score quizzes.

## Responsible AI risks

| Risk | Possible harm | Planned control |
|---|---|---|
| Wrong answer or weak supporting evidence | A student learns an incorrect fact. | Show the source passage and page; require human acceptance before quiz use. |
| Two correct options or confusing wording | A student receives an unfair or misleading question. | Flag repeated or missing options and possible ambiguity; allow editing and rejection. |
| Over-trusting a check result | A draft is treated as reliable without review. | Keep Draft and Accepted states separate; do not let automated checks approve questions. |
| Wrong course material is used | Practice questions cover the wrong course. | Search only the chosen course files and show the file name for every question. |
| Private information or restricted notes are shared | Personal information or protected material reaches another service. | Use permitted notes, check sensitive fields and ask permission before sending selected passages. Keep keys and private files out of GitHub. |

## Why GitHub

GitHub will keep the project documents, code, prompts and later test results together. Its history will show what changed and why. The repository is [adamiskandarr05/NOTE2QUIZ](https://github.com/adamiskandarr05/NOTE2QUIZ).
