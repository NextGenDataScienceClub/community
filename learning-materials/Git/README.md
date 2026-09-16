# Data Science Club: Git & GitHub Engineering Guidelines

This workshop is designed for university Data Science Club members who want a practical, production-ready workflow for versioning code, collaborating on notebooks, and shipping analyses responsibly. The goal is not only to learn Git syntax, but to develop habits that help teams work safely, review code effectively, and keep research reproducible.

## Workshop Overview

The session is structured as a 90-minute guided lab with short concept explanations and hands-on terminal practice.

| Time | Module | Focus |
| --- | --- | --- |
| 0-10 min | Kickoff | Why Git matters in data science and engineering |
| 10-25 min | [01: Git Fundamentals](./01-git-fundamentals.md) | Repository architecture, setup, staging, commits |
| 25-45 min | [02: Branching and Merging](./02-branching-and-merging.md) | Feature branches, merge strategies, conflict resolution |
| 45-60 min | [03: Collaboration and PRs](./03-collaboration-and-pr.md) | Remotes, GitHub workflow, reviews, etiquette |
| 60-75 min | [04: Data Science Best Practices](./04-data-science-best-practices.md) | Notebooks, secrets, data, reproducibility |
| 75-90 min | [05: Interactive Resources](./05-interactive-resources.md) | Practice, troubleshooting, and follow-up learning |

## Prerequisites

Before the workshop, make sure you have:

- Git CLI installed locally
- A GitHub account with access to the club or project repository
- SSH keys configured, or a GitHub Personal Access Token for HTTPS
- A shell or terminal available on your machine
- A basic understanding of file systems and command line usage

### Verify your setup

```bash
git --version
ssh -T git@github.com
```

If SSH is not configured, use the GitHub credential helper or personal access token.

## Module Map

- [01: Git Fundamentals](./01-git-fundamentals.md)
- [02: Branching and Merging](./02-branching-and-merging.md)
- [03: Collaboration and Pull Requests](./03-collaboration-and-pr.md)
- [04: Data Science Best Practices](./04-data-science-best-practices.md)
- [05: Interactive Resources](./05-interactive-resources.md)
- [.gitignore Example](./.gitignore.example)

## Expected Learning Outcomes

By the end of the workshop, each member should be able to:

- Explain the difference between the working directory, staging area, local repository, and remote repository.
- Initialize a repository, clone an existing project, and configure Git for personal use.
- Create commits with meaningful, conventional messages and inspect commit history.
- Use branches to isolate work, merge updates safely, and resolve simple conflicts.
- Push code to GitHub, open a pull request, and participate in code review feedback.
- Protect sensitive data and notebooks using .gitignore, environment variables, and reproducibility tooling.
- Recognize the difference between normal developer workflows and data science repository hygiene.

## Recommended Workflow for Club Members

1. Create a branch for each task or experiment.
2. Keep commits small and meaningful.
3. Write useful commit messages and PR descriptions.
4. Do not commit raw data, credentials, or notebook outputs.
5. Review changes before merging.
6. Keep your environment reproducible with pinned dependencies.

## Quick Start

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.edu"
git config --global init.defaultBranch main
git config --global core.editor "code --wait"
```

Then choose a project and start with:

```bash
git clone <repository-url>
cd <repository-name>
git status
```

## Additional Notes

This curriculum is intentionally designed for students who may be new to version control but are already working with notebooks, scripts, models, and collaborative analysis. The guidance in these modules emphasizes correctness, safety, and reproducibility more than speed.

---

For the full learning path, start with [01: Git Fundamentals](./01-git-fundamentals.md).
