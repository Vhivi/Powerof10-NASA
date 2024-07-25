# Contribution Guide for Adding a Programming Language Adaptation of NASA Rules

- [Contribution Guide for Adding a Programming Language Adaptation of NASA Rules](#contribution-guide-for-adding-a-programming-language-adaptation-of-nasa-rules)
  - [Getting Started](#getting-started)
  - [Guidelines for Adding a New Programming Language Adaptation](#guidelines-for-adding-a-new-programming-language-adaptation)
  - [Guidelines for Modifying Existing Files](#guidelines-for-modifying-existing-files)
  - [Code of Conduct](#code-of-conduct)

Thank you for your interest in contributing to our Powerof10-NASA repository. We are happy to accept additional programming language adaptations for NASA rules. Please follow the steps below to submit your contribution:

## Getting Started

1. Fork the repository.

2. Clone your fork: `git clone https://github.com/your-username/Powerof10-NASA.git`

    :warning: Replace `your-username` with your GitHub username. :warning:

3. Create a branch for your changes:
   - For new files: `git checkout -b add-new-rules-{proglang}`
   - For modifications: `git checkout -b modify-existing-docs-{proglang}`

4. Make your changes, the naming convetion is `Powerof10-{proglang}.md`.

5. Commit your changes, we try to use the [Conventional Commits specifications](https://www.conventionalcommits.org/):
   - For new files: `git commit -m "feat: add new rules for {proglang}"`
   - For modifications: `git commit -m "docs(Powerof10-{proglang}): modify existing documentation for {proglang}"`

6. Push to your branch: `git push origin add-new-rules-{proglang}` (or `modify-existing-docs-{proglang}`).

7. Open a pull request:
   - For new files: "Add new rules for {proglang}"
   - For modifications: "Modify existing documentation for {proglang}"

8. Wait for your pull request to be reviewed and merged.

:construction: Make sure to replace {proglang} by the language you want to add. :construction:

We will review your contribution as soon as possible and provide feedback if necessary.

Thank you for your contribution!

## Guidelines for Adding a New Programming Language Adaptation

1. Before you start, make sure you read the NASA rules for the C programming language in the file `rules/Powerof10-C.md`. This will give you an idea of the rules you will need to adapt for your programming language. This is the reference file for the NASA rules.

2. Create a new Markdown file in the `rules/` directory using the naming format `Powerof10-{proglang}.md`, where `{proglang}` is the name of your programming language. For example, if you adapt the rules for Python, the file name will be `Powerof10-Python.md`.

3. In the file you have just created, adapt the NASA rules for your programming language. Make sure you follow the same format as that used in the `examples/Powerof10-Template.md` file. This allows you to have the rules in the same order, a reminder of the original rule and also examples to avoid and recommend. You can add comments or additional explanations if necessary.

4. Finally, submit your contribution by creating a pull request to the main branch of the repository. Make sure you provide a clear description of your contribution and mention any changes you have made.

We will review your contribution as soon as possible and provide feedback if necessary.

Thanks again for your contribution!

## Guidelines for Modifying Existing Files

1. Make sure to update the relevant sections without breaking the existing structure.

2. Provide clear and concise commit messages.

## Code of Conduct

Please note that this project is released with a Contributor Code of Conduct. By participating in this project you agree to abide by its terms.
