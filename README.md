# Python Project Template

This is a fork of [voraus-python-template](https://github.com/vorausrobotik/voraus-python-template).
It helps to quickly spin up Python projects via [cookiecutter](https://github.com/cookiecutter/cookiecutter) and [cruft](https://github.com/cruft/cruft/).

## Getting Started

Create a new virtual environment and install necessary dependencies.

```
python -m venv venv
source venv/bin/activate
pip install cruft ruff cookiecutter
```

## Creating a New Project

Create a new project with

```
cruft create git@github.com:Mr-Pepe/python-template.git
```

and follow the prompts. The template will ask you for a name and email address to use for the maintainer of the project (the name and email address of your active Git profile is used by default).
Unless you know what you are doing, you should define a project name, e.g., "My Project", and go with the proposed default values.
Cruft uses [cookiecutter](https://cookiecutter.readthedocs.io/en/1.7.3/installation.html#install-cookiecutter) behind the scenes to generate the project.


## Updating an Existing Project

Cruft helps with updating projects that were originally created from a template.
Run `cruft check` to check whether the project is out of sync with the template.
Run `cruft update` to update the project.
The update is performed by looking at the template branch that is specified as `checkout` in the `cruft.json`.

## Working on Projects

Python projects created with the template come pre-configured with an extensive CI pipeline.

[tox](https://tox.readthedocs.io/en/latest/) makes it easy to run the full CI pipeline on your local machine.
The minimal setup to develop your package is to create a virtual environment and install the package and its runtime requirements:

```
python -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -e .[dev]
```

### Run tests

Run `tox run` to execute the test pipeline. The tox pipelines are configured in the `tox.ini` file. Configurations for specific tools in the pipeline are maintained in the `pyproject.toml` file. tox is configured to create its own virtual environments, install test dependencies and the package you are developing, and run all tests. If you want to perform a clean run for some reason, you can run `tox run -r` to recreate tox's virtual environment.

The following tools are part of the test pipeline:

[mypy](https://mypy.readthedocs.io/en/stable/): Statically checks your type hints.

[ruff](https://github.com/astral-sh/ruff): Formats your code, orders your imports, statically checks your code and docstrings for errors and code smells.

[pytest](https://docs.pytest.org/en/): Provides a framework for unit tests. Also doc-tests your docstrings and collects coverage information via pytest-cov.

If you don’t want to run the whole test pipeline, you can also use single commands from the pipeline, e.g., `pytest`.
The tools will automatically pick up the correct configuration from the pyproject.toml file.

### Build the documentation

Run `tox run -e docs` to build your documentation with Sphinx straight from your code.
You can add additional documentation inside the `docs/` folder.
The pipeline also runs doctests that you added in the documentation (.rst files).
Doctests inside your code's docstrings are executed by pytest.

The Sphinx-native autodoc extension converts Python docstrings to RST.
It imports the modules to be documented.
If any modules have side effects on import, these will be executed by autodoc when sphinx-build is run.
Scripts (as opposed to library modules) must therefore be protected by an `if __name__ == '__main__'` condition.

### Build the package

Run `tox run -e build` to build your package. The resulting wheel and sdist can be found in the `dist` folder.

## Improving This Template

You need to make the desired changes **in the template** (the `{{cookiecutter.repo_name}}` folder).
Don't accidentally make your changes in the generated project (the `cookiecutter-pypackage` folder) because
those changes will be overridden again.
Commit your changes so that they are used for the template generation in the next steps.
Non-committed changes won't be added to the template!
Run `tox run` from the repo's root folder to use the template to generate the sample package with your new changes.
Change into the generated folder and run `tox run`, `tox run -e docs`, and `tox run -e build` to check that your changes
work with the sample package.
(Amend-)commit again and push all changes.

## License Notices

This project is licensed under the [MIT License](https://opensource.org/license/mit/).
