# perfect-bioinformatic-tools

What should perfect bioinformatic tools be like?

## General principles

- Reproducible
- Installable
- User-friendly

## Installation

Basic

- Dependency specification
    - Specifying the lowest version AND highest version.
      For example, some standard libraries in Python 3.10 have compatibility problems.

Recommended

- Supporting Conda/Pip
- Providing static-linked executable binary files for multiple operating systems/platforms
- Compiling from source

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
    - Avoiding hard-coded paths/parameters

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

Recommended

- Supporting shell auto-completion
- Checking the latest version

### Input

Basic

- Supporting input file list
- Validating option values

Recommended

- Optional supporting input directory
- Seamless support of common compression files
- Checking flag/option incompatibility

Ideal

- Checking files before performing processing

### Output

Basic

- Showing overwrite warning

Recommended
  
- Seamless support of common compression files

### Log

Recommended

- Optionally outputting in stderr and/or a file.
- Progress bar for a list of files/jobs

Log details

- Command and its version
- Time and memory usage
- Flags, arguments, and options
