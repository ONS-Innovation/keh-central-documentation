# KEH Central Documentation

This repository contains a centralised place for common documentation within KEH.

## Table of Contents

- [AWS](/aws)
  - [Commands](/aws/COMMANDS.md) (Commands related to AWS such as installing the CLI, configuring the CLI with/out profiles etc.)
  - [ECR](/aws/ECR.md) (Specific commands related to ECR such as login, push, pull, etc.)
- [documentation](./documentation/)
  - [mkdocs_and_pages.md](./documentation/mkdocs_and_pages.md) (Documentation on how to use MkDocs and GitHub Pages)
- [misc](./misc/)
  - [Versioning](./misc/VERSIONING.md) (Versioning strategy for KEH)
- [Templates](/templates)
  - [PR Template](./templates/pull_request_template.md) (Pull request template for a repository)
  - [Example README](/templates/README.example.md) (README example template for a repository)
  - [README](/templates/README.md) (README remplate for a repository)
- [Terraform](/terraform)
  - [Commands](/terraform/COMMANDS.md) (Commands related to Terraform such as init, plan, apply, etc.)

## Contributing

1. Clone the repository:

    ```bash
    git clone https://github.com/ONS-Innovation/keh-central-documentation.git
    ```

2. Create a new branch:

3. Once ready, create a pull request.

4. Request a review from the [keh-dev](https://github.com/orgs/ONS-Innovation/teams/keh-dev) team.

## Markdownlint-cli

This repository uses [markdownlint-cli](https://github.com/igorshubovych/markdownlint-cli) to lint markdown files.

Markdownlint-cli is a command line interface for [MarkdownLint](https://github.com/DavidAnson/markdownlint).

### Markdownlint Prerequisites

Markdownlint-cli requires Homebrew to be installed.

### Markdownlint Setup

Run Markdownlint-cli in a container:

```bash
docker run -v $PWD:/workdir ghcr.io/igorshubovych/markdownlint-cli:latest "*.md"
```

or install Markdownlint-cli locally:

```bash
brew install markdownlint-cli
```

### Markdownlint Usage

Lint all markdown files:

```bash
markdownlint .
```

Fix all markdown files:

```bash
markdownlint --fix .
```

### `.markdownlint.json` Configuration

The `.markdownlint.json` file in the root of the repository contains the configuration for markdownlint. This file is used to set the rules and settings for linting markdown files.

Currently, MD013 (line length) is disabled. This is because the default line length of 80 characters is too restrictive.

For a full list of rules, see [Markdownlint Rules / Aliases](https://github.com/DavidAnson/markdownlint?tab=readme-ov-file#rules--aliases)

### Markdownlint GitHub Action

This repository uses GitHub Actions to run markdownlint on every push and pull request. The workflow file is located in the `.github/workflows` directory.

The workflow will run markdownlint on all markdown files in the repository. If any linting errors are found, the workflow will fail and provide a report of the errors.
