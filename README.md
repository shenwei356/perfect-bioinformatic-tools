# Perfect bioinformatic tools

What should perfect bioinformatic tools be like?

This page lists some personal suggestions for improving the usability of bioinformatic (command-line) tools.

## General principles

- **Accurate**. This should be the most essential aspect, at least for simple analysis. While there may be occasional bugs, regular updates and bug fixes will make the tool more accurate and reliable over time. 
- **Reproducible**. That means users can reproduce the same result with the same input data, the same version of the tool, and the same parameters (assuming the program is [deterministic](https://en.wikipedia.org/wiki/Deterministic_algorithm)).
- **Installable**. Some tools run perfectly on developers' computers, while users with different platforms might struggle to install them, the failure might be due to different dependencies, hard-coded paths, etc.
- **User-friendly**. A tool should be easy to use, with comprehensive documents and well-handled configuration/input/output.
- **Long-time maintenance**. Bug fixes, adding new features, accuracy and usability improvement.
  [Sustained software development, not number of citations or journal choice, is indicative of accurate bioinformatic software](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-022-02625-x).

## Installation

Basic

- **Specifying dependencies**.
    - Specifying the lowest version AND the highest version.
      For example, some standard libraries in Python 3.10 have compatibility problems.
- **Providing sample/test data**. To verify the tool is successfully installed.

Recommended to provide all ways:

- **Supporting Conda/Pip**. IMO, this should be a mandatory requirement for ready-for-publication tools.
    - Automatically installing all library and 3rd-party dependencies.
- **Providing static-linked executable binary files** for multiple operating systems/platforms. Some tools written in C++ are difficult to compile from source, and dynamic-linked binaries often fail to run in clusters with older libraries, e.g., `version 'GLIBC_2.29' not found` is a common error.
- **Compiling from source**. Some servers might have rare CPUs or operating systems, users have to compile from source.

## Documentation

Basic

- **Quickstart with sample data**.
- **Usages for all commands**.
    - **Specifying the input requirements in detail**.
- **Change history**, including semantic versions, dates, and changes. This helps users learn the update details and also shows that the project is actively maintained.

Recommended

- Tutorials for common scenarios.
- FAQs for common operations and mistakes.
- Third-party tools and their links.

Ideal

- **Stories behind the development and publication**. This is inspiring for students, e.g., [C. Titus Brown shares many stories behind sourmash and his other tools](http://ivory.idyll.org/blog/),
  [Developing sylph - a look into bioinformatics tool development](https://jim-shaw-bluenote.github.io/blog/2024/developing-sylph/),

## Source code

- **Scripts should be compatible with multiple interpreters**. E.g., Python 2 and 3, and some standard libraries in Python 3.10 have compatibility problems. Snakemake's command-line flags also change a lot, e.g., in 7.x versions.
- **Code comments**
    - **Providing essential comments for reviewers/users to understand the logic**.
    - Providing detailed comments for developers/contributors to know the details.
- **Version control**
- Configuration file
    - **Avoiding hard-coded absolute paths/lib/packages/parameters in source code**
- Unit tests. To make the tool robust.

## Version control

- [**Semantic Versioning**](https://semver.org/). Please do follow this. Many tools release a V1.0 and never update it again.
- [**Preserving each release with Zenodo**](https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content). This is recommended for all tools, which make sure readers can reproduce the analysis.

## Command-line tools

### Architecture

- **Using command-subcommand structure for toolkits with multiple commands**. It is convenient for fast locating subcommands without checking the official documents.

Options/flags

- **Using common flags**. E.g., `-o, --outfile` for output.
- **Using both short and long forms**. Adding short forms for frequently used flags.
- Using consistent flags in multiple subcommands.

Global options/flags

- `--quiet` or `--verbose`
- `--version`
- `--log`

### Misc

Recommended

- **Supporting shell auto-completion**. This could significantly improve the usability of toolkits.
- Checking the latest version.
- Handling Ctrl+C.

### Input

Basic

- **Supporting input file list**. Things happen a lot when users give hundreds of input files, which would exceed the argument length limit of some shells.
    - **Supporting file list from stdin**. This is a good feature. e.g., `find ./ -name "*.fq.gz" | tool cmd --infile-list -`.
- **Validating ALL option values first**. No one would like to see the process fail midway, caused by an invalid option which is parsed and used in some middle steps.

Recommended

- **Supporting stdin**. This enables commands to pipe up as a workflow.
    - Supporting both stdin and command-line arguments would be useful in some cases.
- Optional supporting input directory, for tools requiring multiple input files.
- **Optionally accepting and skipping empty files**. For example, in a workflow, some upstream tools might output an empty file because there's no result to write. Current tools should tolerate it and just exit without error.
- **Seamless support of common compression files**. At least gzip. And compression format checking should be based on the magic number, not the file extension. 
- **Checking flag/option incompatibility and showing warnings before starting the jobs**.

Ideal

- **Checking file existence before performing processing**. It happens frequently when a long-time job is terminated by one nonexistent input file.
    - This checking can be cancelled for cases where the users trust that all input files exist. Because checking thousands of input files would take a long time.
- **Checking if the input file/directory and output file/directory are the same one**. If they are, the input file might be overwritten. And *the paths should be converted to absolute paths before comparison, rather than simply checking if two strings are equal*. *Symbolic links (soft links) should be taken into consideration as well*.
- **If paired-end files are accepted as input, check that the user didn't accidentally provide the same file to both R1 and R2 arguments**. If so, inform and exit immediately.

### Output

Basic

- **Supporting both stdout and the output file**.
- **Showing directory overwrite warning**.
- **Creating the output directory tree automatically if it does not exist**.
- **Writing the output file even if there is no result**. This is important in workflow, where downstream tools need an input file from the upstream tool and the workflow software needs to check the execution status based on the output file.
    - Ideally, **opening the file handler at the beginning**, just in case the output directory does not exist or it is not writable.

Recommended
  
- **Seamless support of common compression files**. Determining the compression format according to the file extension.

### Logging

Recommended

- **Optionally outputting in stderr and/or a file**.
- **Showing a progress bar for a large number of files/jobs and estimating the time of arrival (ETA)**.
- **Checking if the log file and output/input files are the same**.

Log details

- Command and its version
- Time and memory usage
- Flags, arguments, and options
