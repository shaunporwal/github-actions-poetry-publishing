# Poetry Python Package Testing & Publishing Action

![GitHub Action Status](https://img.shields.io/github/workflow/status/YOUR_USERNAME/poetry-publish-action/Poetry%20Python%20Package%20Testing%20&%20Publishing)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A GitHub Action that automates the testing and publishing of Python packages using Poetry. This action handles testing across multiple Python versions and manages publishing to both TestPyPI and PyPI with version checks to prevent duplicate uploads.

## Features

- 🧪 Automated testing across multiple Python versions (3.10, 3.11)
- 📦 Automatic publishing to TestPyPI on main branch pushes
- 🚀 Automatic publishing to PyPI on tag releases
- ✅ Version conflict prevention with pre-publish checks
- 🔄 Conditional publishing based on version existence
- 🛠️ Poetry-based dependency management and publishing

## Usage

Add this workflow to your repository by creating a `.github/workflows/poetry-publish.yml` file:

```yaml
name: Test and Publish

on:
  push:
    branches: [ main ]
    tags: [ '*' ]
  pull_request:

jobs:
  test-and-publish:
    uses: shaunporwal/poetry-publish-action@v1
```

### Prerequisites

1. A Python project using Poetry for dependency management
2. A `pyproject.toml` file in your repository root
3. API tokens for TestPyPI and PyPI (for publishing)

### Setting up API Tokens

1. Create an API token on [TestPyPI](https://test.pypi.org/manage/account/token/)
2. Create an API token on [PyPI](https://pypi.org/manage/account/token/)
3. Add these tokens to your repository secrets:
   - `TEST_PYPI_API_TOKEN`
   - `PYPI_API_TOKEN`

## Workflow Details

### Testing

- Runs automatically on pull requests and pushes to main
- Tests your package against Python 3.10 and 3.11
- Uses Poetry to install dependencies and run pytest

### Publishing to TestPyPI

- Triggers on pushes to the main branch
- Checks if version already exists
- Skips publishing if version is already present
- Requires `TEST_PYPI_API_TOKEN` secret

### Publishing to PyPI

- Triggers when a tag is pushed
- Checks if version already exists
- Skips publishing if version is already present
- Requires `PYPI_API_TOKEN` secret

## Example Project Structure

```
your-python-package/
├── .github/
│   └── workflows/
│       └── poetry-publish.yml
├── src/
│   └── your_package/
│       └── __init__.py
├── tests/
│   └── test_your_package.py
├── pyproject.toml
└── README.md
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
