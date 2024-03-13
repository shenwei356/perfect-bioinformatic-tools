# Perfect bioinformatic tools

What should perfect bioinformatic tools be like?

This page lists some personal suggestions for improving the usability of bioinformatic (command-line) tools.

## General principles

- **Accuate**. This should be the most essential aspect.
- **Reproducible**. That means users can reproduce the same result with the same input data, the same version of the tool, and the same parameters.
- **Installable**. Some tools run perfectly on developers' computers, while users with different platforms might struggle to install them, the failure might be due to different dependencies, hard-coded paths, et.al.
- **User-friendly**. A tool should be easy to use, with comprehensive documents and well-handled configuration/input/out.
- **Long-time maintenance**. [Sustained software development, not number of citations or journal choice, is indicative of accurate bioinformatic software](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-022-02625-x).

## Installation

Basic

- **Specifying dependencies**.
    - Specifying the lowest version AND highest version.
      For example, some standard libraries in Python 3.10 have compatibility problems.
- **Providing sample data**.

Recommended to provide all ways:

- **Supporting Conda/Pip**. IMO, this should be a mandatory requirement for ready-for-publication tools.
    - Automatically installing all dependencies
- **Providing static-linked executable binary files** for multiple operating systems/platforms. Some tools written in C++ are difficult to compile from source, and dynamic-linked binaries often fail to run in clusters with older libraries.
- **Compiling from source**. Some servers might have rare CPUs or operating systems, users have to compile from source.

## Documentation

Basic

- **Quickstart with sample data**.
- **Usages for all commands**.
    - **Specifying the input requirements in detail**.

Recommended

- Tutorials for common scenarios.
- FAQs for common operations and mistakes.
- Dependencies and their links.

Ideal

- **Stories behind the development and publication**. This is inspiring for students, e.g., [C. Titus Brown shares many stories behind sourmash and his other tools](http://ivory.idyll.org/blog/)

## Source code

- Code comments
    - **Providing essential comments for reviewers/users to understand the logic**.
    - Providing detailed comments for developers/contributors to know the details.
- **Version control**
- Configuration file
    - **Avoiding hard-coded paths/lib/packages/parameters**
- Unit tests.

## Version control

- [**Semantic Versioning**](https://semver.org/). Please do follow this. Many tools just release a V1.0 and never update it again.
- [**Preserving each release with Zenodo**](https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content). This is recommended for all tools, which make sure readers can reproduce the analysis.

## Command-line tools

### Architecture

- **Using command-subcommand structure for toolkits with multiple commands**. It is convenient for fast locating subcommands without checking the official documents.

Options/flags

- **Using common flags**. E.g., `-o, --outfile` for output.
- Using both short and long forms.
- Using consistent flags in multiple subcommands.

Global options/flags

- `--quiet` or `--verbose`
- `--version`
- `--log`

### Misc

Recommended

- **Supporting shell auto-completion**. This could significantly improve the usability of toolkits.
- Checking the latest version

### Input

Basic

- **Supporting input file list**. Things happen a lot when users give hundreds of input files which would exceed the argument length limit of some shells.
    - **Supporting file list from stdin**. This is a good feature. e.g., `ls dir | tool cmd --infile-list -`.
- **Validating ALL option values first**. No one would like to see the process fail midway, caused by an invalid option parsed and used in some middle steps.

Recommended

- **Supporting stdin**. This enables commands to pipe up as a workflow.
- Optional supporting input directory, for tools requiring multiple input files.
- **Seamless support of common compression files**. At least gzip.
- **Checking flag/option incompatibility and showing warnings before starting the jobs**.

Ideal

- **Checking file existence before performing processing**. It happens frequently when a long-time job is terminated by one unexisting input file.
    - This checking can be cancelled for cases where the users trust all input files exist. Because checking thousands of input files would take a long time.
- **Checking if the input file/directory and output file/directory are the same one**. If they are, the input file might be overwritten.

### Output

Basic

- **Supporting both stdout and the output file**.
- **Showing overwrite warning**.

Recommended
  
- **Seamless support of common compression files**.

### Logging

Recommended

- **Optionally outputting in stderr and/or a file**.
- **Showing a progress bar for a large number of files/jobs and estimating the time of arrival (ETA)**.

Log details

- Command and its version
- Time and memory usage
- Flags, arguments, and options
