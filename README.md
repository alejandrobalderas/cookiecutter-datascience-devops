# Cookiecutter Data Science with Docker

## Requirements

- Python 3.5 or later
- Cookiecutter 1.6 or later
- Docker 20 or later

### Cookiecutter Requirements

## Start a new project

---

From the command line run

```bash
cookiecutter https://github.com/alejandrobalderas/cookiecutter-datascience-docker
```

This will ask you several questions of your project. This include:

- "project_name": This will be your project name and the name of the directory that will be created,
- "repo_name": Uses the project name as default with no spaces and underscores
- "author_name": Your name
- "description" : This will be used in your README file
- "python_version" : Choose which version of python you want to run. This will pull the corresponding docker image and use this version in the Pipfile. The python version could be change later on so it would be advised to take the latest available
- "jupyter_port" : This will map the port inside of the container to the chosen port in your local computer. Choose a port that is not being used.

## Using with Docker

To create your container and start your development environment you can use the following Makefile targets

### init

Builds the base image and sets the environment. This include installing the dependencies specified in the Pipfile

```bash
make init
```

### jupyter

Starts a container running jupyter lab in your specified port. You can start do your

```bash
make jupyter
```

### Default packages

This will install all packages inside of the Pipfile which by default include the following:

- pandas
- numpy
- scikit-learn
- scipy
- jupyterlab
- seaborn
- matplotlib
- statsmodels
- python-dotenv

If you want to install aditional packages you can run

```bash
pipenv install [name of your package]
```

or alternatively edit the Pipfile and just `pipenv install`.

If you want to install a package within the jupyter notebook you can just add the `!` and type a command as if you were using your shell. Example `! pipenv install [name of your package]`

The virtualenv will also install the src directory as a python package. You can import it from every file in your project without needing to worry about the path.
