# {{ cookiecutter.project_name }}

{{cookiecutter.description}}

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

### bash

Run bash inside of the container.

```bash
make bash
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

## Project Organization

    ├── Makefile            <- Makefile with relevant commands to use in this project
    ├── README.md           <- What you should read before going to the src code.
    ├── data
    │   ├── raw             <- Data in its raw form
    │   └── processed       <- Transformed data (raw -> cooked)
    │
    ├── models              <- Trained and serialized models.
    │
    ├── notebooks           <- Jupyter notebooks.
    │
    ├── docs                <- All relevant documents for documentation and reports.
    │
    ├── Pipfile             <- Using pipfile to manage package inside the project
    │
    ├── main.py             <- Can be used as main entry point for the docker container to run
    ├── setup.py            <- Makes the src directory installable as a python package
    ├── src                 <- Source code of the project
    │   ├── __init__.py     <- Makes src a Python module

---
