# Blaise NiFi notify

This repository contains a Google Cloud Function designed to create and publish metadata to a Pub/Sub topic when a zip file is uploaded to a Google Cloud Storage bucket.

The workflow is as follows:

1.  A zip file is uploaded to a specific GCS bucket.
2.  The upload event triggers this Cloud Function.
3.  The function validates the file's name and generates a metadata message.
4.  This metadata message is published to a Google Cloud Pub/Sub topic.

This process is designed to integrate with NiFi downstream services, which then consume these messages to transfer and process the files on-premises.

For the function to process a file, the uploaded zip file must be prefixed with either `mi_` (for Management Information) or `dd_` (for Data Delivery). The filename should also be unique, typically by including a timestamp.

For example: `mi_opn2001a_01012020_1200.zip`

## Local Development Setup

Prerequisites:

- Python
- Poetry
- Git

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/ONSdigital/blaise-nifi-notify.git
    cd blaise-nifi-notify
    ```

2.  **Install dependencies:**
    This project uses Poetry for dependency management. The following command will create a virtual environment and install all necessary packages.
    ```bash
    poetry install
    ```

## Running Development Tasks

This project includes a `Makefile` with common development commands.

-   **Format:**
    Formats the code using `black` and `isort`.
    ```bash
    make format
    ```

-   **Lint:**
    Checks for code quality, style issues, and type errors.
    ```bash
    make lint
    ```

-   **Test:**
    Executes the test suite using `pytest`.
    ```bash
    make test
    ```

## Virtual Environment

Poetry automatically manages the project's virtual environment. If you need to find the path to the Python interpreter within this environment (for example, to configure your IDE), you can use the following command:

```bash
echo "$(poetry env info --path)/bin/python"
```

This will output the full path to the Python executable.
