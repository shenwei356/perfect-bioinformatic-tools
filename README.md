# perfect-bioinformatic-tools

What should perfect bioinformatic tools be like?

## General principles

- Reproducible
- Installable
- User-friendly

## Installation

- Providing static-linked executable binary files
- Supporting Conda/Pip
- Compiling from source
- Dependency specification.
    - Specifying the lowest version AND highest version.
      For example, some standard libraries in Python 3.10 have compatibility problems.

## Documentation

- Quickstart
- Usages for all commands
- Tutorials for common scenarios
- FAQs for common operations and mistakes

## Source code

- Code comments
    - Providing essential comments for reviewers/users to understand the logic
    - Providing detailed comments for developers/contributors to know the details
- Version control
- Configuration file
    - Avoid hard-coded paths/parameters

## Version control

- [Semantic Versioning](https://semver.org/)
- [Preserving each release with Zenodo](https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content).

## Command-line tools

### Architecture

- Command-subcommand structure for easily locating subcommand

Global options

- `--quiet` or `--verbose`
- `--version`

### Misc

- Supporting shell auto-completion
- Checking the latest version

### Input

- Supporting input file list
- Optional supporting input directory
- Seamless support of common compression files

### Output

- Overwriting warning
- Seamless support of common compression files
- Log file with details
    - Command and its version
    - Arguments and options
    - Time and memory usage
