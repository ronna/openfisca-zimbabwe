# OpenFisca Zimbabwe


The country whose law is modelled here has a very simple tax and benefit system.

- It has a flat rate tax whose rates increase every year.
- On the first of December, 2015, it introduced a basic income for all its citizens of age who have no income.
- On the first of December, 2016, it removed the income condition, providing all its adult citizens with a basic income.

These elements are described in different folders. All the modelling happens within the `openfisca_zimbabwe` folder.

- The rates are in the `parameters` folder.
- The formulas are in the `variables` folder.
- This country package comes also with *reforms* in the `reforms` folder. This is optional: your country may exist without defining any reform.
    - In this country, there is [a reform project](./openfisca_zimbabwe/reforms/modify_social_security_taxation.py) aiming to modify the social security taxation, deleting the first bracket, raising the intermediary ones and adding a new bracket with a higher tax rate of `40 %` for people earning more than `40000`. This reform project would apply starting from `2017-01-01`.

The files that are outside from the `openfisca_zimbabwe` folder are used to set up the development environment.

## Packaging your Country Package for Distribution

Country packages are python distributions. To distribute your package via `pip`, follow the steps given by the [Python Packaging Authority](https://python-packaging-user-guide.readthedocs.io/tutorials/distributing-packages/#packaging-your-project).

## Install Instructions for Users and Contributors

This package requires [Python 3.9](https://www.python.org/downloads/release/python-390/). More recent versions should work, but are not tested.

All platforms that can execute Python are supported, which includes GNU/Linux, macOS and Microsoft Windows.

### Setting-up a Virtual Environment with venv

In order to limit dependencies conflicts, we recommend using a [virtual environment](https://www.python.org/dev/peps/pep-0405/) with [venv](https://docs.python.org/3/library/venv.html).

- A [venv](https://docs.python.org/3/library/venv.html) is a project specific environment created to suit the needs of the project you are working on.

To create a virtual environment, launch a terminal on your computer, `cd` into your directory and follow these instructions:

```sh
python3 -m venv openfisca # create a new venv called “openfisca”
source openfisca/bin/activate # activate the venv
```

You can now operate in the venv you just created.

You can deactivate that venv at any time with `deactivate`.

:tada: You are now ready to install this OpenFisca Country Package!

Two install procedures are available. Pick procedure A or B below depending on how you plan to use this Country Package.

### A. Minimal Installation (Pip Install)

Follow this installation if you wish to:
- run calculations on a large population;
- create tax & benefits simulations;
- write an extension to this legislation (e.g. city specific tax & benefits);
- serve your Country Package with the OpenFisca Web API.

For more advanced uses, head to the [Advanced Installation](#advanced-installation-git-clone).

#### Install this Country Package with Pip Install

Inside your venv, check the prerequisites:

```sh
python --version  # should print "Python 3.9.xx".
```

```sh
pip --version  # should print at least 9.0.
# if not, run "pip install --upgrade pip"
```
Install the Country Package:

```sh
pip install openfisca_zimbabwe
```

:warning: Please beware that installing the Country Package with `pip` is dependent on its maintainers publishing said package.

:tada: This OpenFisca Country Package is now installed and ready!

#### Next Steps

- To learn how to use OpenFisca, follow our [tutorials](https://openfisca.org/doc/).
- To serve this Country Package, serve the [OpenFisca web API](#serve-your-country-package-with-the-openFisca-web-api).

Depending on what you want to do with OpenFisca, you may want to install yet other packages in your venv:
- To install extensions or write on top of this Country Package, head to the [Extensions documentation](https://openfisca.org/doc/contribute/extensions.html).
- To plot simulation results, try [matplotlib](http://matplotlib.org/).
- To manage data, check out [pandas](http://pandas.pydata.org/).

### B. Advanced Installation (Git Clone)

Follow this tutorial if you wish to:
- create or change this Country Package's legislation;
- contribute to the source code.

#### Clone this Country Package with Git

First, make sure [Git](https://www.git-scm.com/) is installed on your machine.

Set your working directory to the location where you want this OpenFisca Country Package cloned.

Inside your venv, check the prerequisites:

```sh
python --version  # should print "Python 3.9.xx".
```

```sh
pip --version  # should print at least 9.0.
# if not, run "pip install --upgrade pip"
```
Clone this Country Package on your machine:

```sh
git clone https://github.com/openfisca/openfisca-zimbabwe.git
cd openfisca-zimbabwe
pip install --editable .[dev]
```

You can make sure that everything is working by running the provided tests with `make test`.

> [Learn more about tests](https://openfisca.org/doc/coding-the-legislation/writing_yaml_tests.html)

:tada: This OpenFisca Country Package is now installed and ready!

#### Next Steps

- To write new legislation, read the [Coding the legislation](https://openfisca.org/doc/coding-the-legislation/index.html) section to know how to write legislation.
- To contribute to the code, read our [Contribution Guidebook](https://openfisca.org/doc/contribute/index.html).

## Serve this Country Package with the OpenFisca Web API

If you are considering building a web application, you can use the packaged OpenFisca Web API with your Country Package.

To serve the Openfisca Web API locally, run:

```sh
openfisca serve --port 5000
```

Or use the quick-start Make command:

```
make serve-local
```

To read more about the `openfisca serve` command, check out its [documentation](https://openfisca.org/doc/openfisca-python-api/openfisca_serve.html).

You can make sure that your instance of the API is working by requesting:

```sh
curl "http://localhost:5000/spec"
```

This endpoint returns the [Open API specification](https://www.openapis.org/) of your API.

:tada: This OpenFisca Country Package is now served by the OpenFisca Web API! To learn more, go to the [OpenFisca Web API documentation](https://openfisca.org/doc/openfisca-web-api/index.html).

You can test your new Web API by sending it example JSON data located in the `situation_examples` folder.

Substitute your package's country name for `openfisca_zimbabwe` below:

```sh
curl -X POST -H "Content-Type: application/json" \
  -d @./openfisca_zimbabwe/situation_examples/couple.json \
  http://localhost:5000/calculate
```
