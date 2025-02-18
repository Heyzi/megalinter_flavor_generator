# MegaLinter Flavor Generator

This script automates the process of generating new MegaLinter flavors. It creates a custom flavor based on selected components (linters) and builds a Docker image for this new flavor.

## Script Logic

1. Update the schema file (megalinter-descriptor.jsonschema.json) to include the new flavor if it doesn't exist.
2. Modify the flavor factory file (flavor_factory.py) to add the new flavor and its description.
3. Update YAML descriptor files in the descriptors directory:

- Add the new flavor to linters specified in the components list.
- Remove the new flavor from linters not in the components list.

4. Run the build.py script to generate necessary files for the new flavor.
5. Build a Docker image for the new flavor using the appropriate Dockerfile.

## Requirements

- Python 3.6+
- Docker
- ruamel.yaml library

## Installation

1. Clone the MegaLinter repository:
```
git clone https://github.com/oxsecurity/megalinter.git
cd megalinter
```
2. Copy this script into the root directory of the cloned repository.
3. Install dependencies: `pip install ruamel.yaml`

## Usage

Run the script from the root of the MegaLinter repository:
```
python3 flavor_generator.py [--new-flavor "FLAVOR_NAME"] [--new-flavor-description "DESC"] [--components "COMP1,COMP2,..."]
```
Arguments:
- `--new-flavor`: Name of the new flavor (default: "devops_light")
- `--new-flavor-description`: Description of the new flavor (default: "Optimized for DevOps pipelines workflows")
- `--components`: Comma-separated list of linter names to include in the flavor. Choose from the "Linter" column at https://megalinter.io/latest/supported-linters/. If not specified, a default set of linters will be used.

### Example
```
python3 flavor_generator.py --new-flavor "devops_light" --new-flavor-description "Optimized for devops pipelines workflows" --components "prettier,npm-groovy-lint,helm,yamllint,sqlfluff,gitleaks,secretlint,trivy,pylint,black,flake8,isort,bandit,mypy,pyright,kubescape,ruff,hadolint,ansible,bash-exec,shellcheck,shfmt,jscpd"
```

## Light version

`flavor_generator_light.py` version reuses some functions from `build.py` to generate only the essential files: `action.yml`, `Dockerfile`, and `flavor.json`.

- This script is significantly faster than the full generation process
- It's not recommended for production use

## Note

Ensure Docker is installed and running before executing the script. BuildKit support is required for Docker image building.

## Error Handling

The script includes comprehensive error handling and logging. Check the console output for any issues during execution.

## Customization

Modify the `DEFAULT_*` variables at the top of the script to change default values for flavor name, description, and components.