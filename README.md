[![CircleCI](https://circleci.com/gh/noosenergy/noos-terraform.svg?style=svg&circle-token=eec3000121ab0ce0659e9c0b2c09347a6e3cd000)](https://circleci.com/gh/noosenergy/noos-terraform)

# Noos Energy Terraform Client

A Python client wrapping up HashiCorp's Terraform Cloud API.

## Installation

Package available from the [PyPi repository](https://pypi.org/project/noos-tf/):

    $ pip install noos-tf

## Usage as a library

Import the namespace within your project,

```python
import os
import noos_tf

# Instantiate client
tf_client = noos_tf.TerraformClient()

# Authenticate client
tf_client.set_auth_header(token=os.getenv("TERRAFORM_TOKEN"))
```

Then query directly from the Terraform Cloud API ; as a example:

* a workspace ID:
```python
tf_client.get_workspace_id("myOrganisation", "myWorkspace")
```

* the variable IDs from a given workspace:
```python
tf_client.get_variable_ids("myOrganisation", "myWorkspace")
```

The library offers as well some helper functions for more involved workflows, such as:

* updating a variable value:
```python
noos_tf.update_workspace_variable(
    "myOrganisation",
    "myWorkspace",
    os.getenv("TERRAFORM_TOKEN"),
    "myVariable",
    "new_value",
)
```

* running and applying a plan:
```python
noos_tf.run_workspace_plan(
    "myOrganisation",
    "myWorkspace",
    os.getenv("TERRAFORM_TOKEN"),
    "Test run",
)
```

## Usage as a command line tool

The above helper functions could be accessed directly from the command line.

```bash
$ noostf

Usage: noostf [--core-opts] <subcommand> [--subcommand-opts] ...

Subcommands:

  run      Run a plan in Terraform cloud.
  update   Update variable in Terraform cloud.
```

### Development

Make sure [poetry](https://python-poetry.org/) has been installed and pre-configured,

This project is shipped with a Makefile, which is ready to do basic common tasks.

```bash
$ make

help                           Display this auto-generated help message
update                         Lock and install build dependencies
clean                          Clean project from temp files / dirs
format                         Run auto-formatting linters
install                        Install build dependencies from lock file
lint                           Run python linters
test                           Run pytest with all tests
package                        Build project wheel distribution
release                        Publish wheel distribution to PyPi
```
