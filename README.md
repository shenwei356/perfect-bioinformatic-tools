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

Options/flags

- Using common flags. E.g., `-o, --outfile` for output.
- Using consistent flags in multiple subcommands.
- Using both short and long forms.

Global options/flags

- `--quiet` or `--verbose`
- `--version`

### Misc

Recommended

- Supporting shell auto-completion
- Checking the latest version

### Input

Basic

- Supporting input file list. Things happen a lot when users give hundreds of input files which would exceed the argument length limit of some shells.
- Validating ALL option values. No one would like to see the process fail midway, caused by an invalid option parsed and used in some middle steps.

Recommended

- Supporting stdin
- Optional supporting input directory
- Seamless support of common compression files
- Checking flag/option incompatibility and showing warnings before starting the jobs.

Ideal

- Checking file existence before performing processing. It happens frequently when a long-time job is terminated by one unexisting input file.
    - This checking can be cancelled for cases where the users trust all input files exist.

### Output

Basic

- Supporting both stdout and the output file.
- Showing overwrite warning

Recommended
  
- Seamless support of common compression files

### Log

Recommended

- Optionally outputting in stderr and/or a file.
- Showing a progress bar for a large number of files/jobs and estimating time of arrival (ETA).

Log details

- Command and its version
- Time and memory usage
- Flags, arguments, and options
