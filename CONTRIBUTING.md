# **PANDORA** **Contributing guide**.

1. [Bug report](#bug-report)
2. [Contributing workflow](#contributing-workflow)
3. [Contribution license agreement](#contribution-license-agreement)
4. [Coding guide](#coding-guide)
5. [Pre-commit validation](#pre-commit-validation)

# Bug report

Any proven or suspected malfunction should be traced in a bug report, the latter being an issue in the PANDORA github repository.

**Don't hesitate to do so: It is best to open a bug report and quickly resolve it than to let a problem remains in the project.**
**Notifying the potential bugs is the first way for contributing to a software.**

In the problem description, be as accurate as possible. Include:
* The procedure used to initialize the environment
* The incriminated command line or python function
* The content of the input and output configuration files (`content.json`)

# Contributing workflow

Any code modification requires a Merge Request. It is forbidden to push patches directly into master (this branch is protected).

It is recommended to open your Merge Request as soon as possible in order to inform the developers of your ongoing work.
Please add `WIP:` before your Merge Request title if your work is in progress: This prevents an accidental merge and informs the other developers of the unfinished state of your work.

The Merge Request shall have a short description of the proposed changes. If it is relative to an issue, you can signal it by adding `Closes xx` where xx is the reference number of the issue.

Likewise, if you work on a branch (which is recommended), prefix the branch's name by `xx-` in order to link it to the xx issue.

PANDORA Classical workflow is :
* Check Licence and sign [Contributor Licence Agrement](#contribution-license-agreement) (Individual or Corporate)
* Create an issue (or begin from an existing one)
* Create a Merge Request from the issue: a MR is created accordingly with "WIP:", "Closes xx" and associated "xx-name-issue" branch
* Modify PANDORA code from a local working directory or from the forge (less possibilities)
* Git add, commit and push from local working clone directory or from the forge directly
* Follow [Conventional commits](https://www.conventionalcommits.org/) specifications for commit messages
* Beware that pre-commit hooks can be installed for code analysis (see below pre-commit validation).
* Launch the tests with [pytest](https://pytest.org) on your modifications (or don't forget to add ones).
* When finished, change your Merge Request name (erase "WIP:" in title ) and ask to review the code.
 

# Contribution license agreement

PANDORA requires that contributors sign out a [Contributor License
Agreement](https://en.wikipedia.org/wiki/Contributor_License_Agreement). The
purpose of this CLA is to ensure that the project has the necessary ownership or
grants of rights over all contributions to allow them to distribute under the
chosen license (Apache License Version 2.0)

To accept your contribution, we need you to complete, sign and email to *cars [at]
cnes [dot] fr* an [Individual Contributor Licensing
Agreement](./docs/source/CLA/ICLA-PANDORA.doc) (ICLA) form and a
[Corporate Contributor Licensing
Agreement](./docs/source/CLA/CCLA-PANDORA.doc) (CCLA) form if you are
contributing on behalf of your company or another entity which retains copyright
for your contribution.

The copyright owner (or owner's agent) must be mentioned in headers of all
modified source files and also added to the [NOTICE
file](./NOTICE).


# Coding guide

Here are some rules to apply when developing a new functionality:
* Include a comments ratio high enough and use explicit variables names. A comment by code block of several lines is necessary to explain a new functionality.
* The usage of the `print()` function is forbidden: use the `logging` python standard module instead.
* Each new functionality shall have a corresponding test in its module's test file. This test shall, if possible, check the function's outputs and the corresponding degraded cases.
* All functions shall be documented (object, parameters, return values).
* Factorize the code as much as possible. The command line tools shall only include the main workflow and rely on the pandora python modules.
* If major modifications of the user interface or of the tool's behaviour are done, update the user documentation (and the notebooks if necessary).
* Do not add new dependencies unless it is absolutely necessary, and only if it has a permissive license.
* Use the type hints provided by the `typing` python module.
* Correct project pylint errors (see below)


# Pre-commit validation

Pre-commit hooks (black, pylint, mypy, sphinx-checking, nbstripout) for code analysis can be installed:
```
pre-commit install
```

This command installs the pre-commit hooks in `.git/hooks/pre-commit`  from `.pre-commit-config.yaml` file configuration.
```
It is possible to test pre-commit before commiting:
* pre-commit run --all-files                # Run all hooks on all files
* pre-commit run --files pandora/__init__.py   # Run all hooks on one file
* pre-commit run pylint                     # Run only pylint hook
```

It is possible to run only pylint tool to check code modifications:
```
* cd PANDORA_HOME
* pylint *.py pandora/*.py tests/*.py        # Run all pylint tests
* pylint --list-msgs                      # Get pylint detailed errors informations
```

Pylint messages can be avoided (in particular cases !) adding "#pylint: disable=error-message-name" in the file or line.
Look at examples in code.


