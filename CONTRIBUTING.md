# Working with SeleniumTestability

## Build & Development Requirements

- nodejs and npm
   - required for downloading and bundling browser code required.
- python >= 3.6
- firefox & chrome
  - webdrivers for both browsers. Instructions to install provided.


## Workflow

First off, you you know what you are doing, go with it but here's
how the project is set up: When all dependencies are installed, all
important tasks to test, build and release can be done via pyinvoke
tool. It's like "make" but, dummer :D  When running `inv` tool to
invoke any of the thse provided tasks, the actual command will be
shown. So that if you want to do something more, you have some
reference on how to extend upon what is being laid down.

Worth to mention is that I tend to work using venv for my dev
environment needs so things might not be optimal for your needs.

Your workflow might differ but i hope you a gist ;D But here's
mine ...


### Generate and activate venv

Clone the repo and cd inside to it and execute following commands:

```bash
python3 -mvenv venv       # Generates the virtual env
source venv/bin/activate  # activates it!
```

### Install dependencies
All project dependencies are listed in root level requirements.txt
and requirements-dev.txt files. These can be used to download and
install into previously activated virtual env via:

```bash
pip install -r requirements-dev.txt
```

This will install all development time dependencies but also runtime
dependencies from requirements.txt file.

## Building and Testing

After all development time dependencies have been installed, your
activated virtual environment shoud have a command `inv` available.
You can give `inv` commands to execute.  These commands provide
shortcuts to runn different tasks like running tests or building
javascript assets to building releases.

In order to know what tasks are currently available:

```bash
inv --list
```

and using one:

```bash
inv flake
```

Some of the tasks can accept parameters. Refer to tasks.py in the
root of the repository and pyinvoke documentation for more details.

At this point, if your shell is activated into virtual environment,
you can add/modify any project file and run existing or add new
tests.

### Build

```bash
inv generatejs
```

#### Test

Before running the tests, you should have chrome & firefox and suitable
webdrivers for both the the browsers. To install webdrivers for *latest* 
browser versions into previously  activated virtual enviroment:

```bash
inv webdrivers
```

After that, run the tests:

```bash
inv test
```

Do note that there are also typing and linting checks that should
pass:

```bash
inv flake mypy rflint
```

### Pull Requests

Yes please! Only thing i ask is that the code follows conventions set
by the provided tooling.

### Release

After verifying that that tests do pass, following comand will make all
necessary preparetions from generating changelog, build docs, change the
version number and commit everything to current branch along with required
version tag:


```bash
inv release --version=VERSION
```

After the release task, use `inv build` to make the release packages and
publish to pypi with `twine`

## Coding Guideles

* mypy checks via `inv mypy` have to pass
* flake8 checks via `inv flake` have to pass
* New features require new tests.
* New tests has to pass `inv rflint`
* Format the code via  `inv black`
