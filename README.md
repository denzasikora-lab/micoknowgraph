# MiCoKnowGraph: Designing a Microbiome Collaborative Knowledge Graph linking complex, multi-domain data

This repository s together scripts for designing a collaborative
microbiome knowledge graph across complex, multi-domain data.

## Repository structure

```text
.
├── data/       # Guidance for inputs, outputs, and data provenance
├── doc/        # Design notes and project documentation
├── scripts/    # Python scripts for the knowledge graph
├── tests/      # Tests for the scripts
└── LICENSE
```

These directories are starting points; no graph-building scripts or datasets
are included yet.

## Getting started

Python 3 is needed to run future Python scripts. To create an isolated
environment from the repository root:

```sh
python3 -m venv .venv
```

Activate it with `source .venv/bin/activate` on macOS or Linux, or
`.venv\Scripts\activate` in Windows Command Prompt. There are currently no
project dependencies to install. Script-specific usage and dependencies
should be documented as scripts are added.

## Contributing

Add scripts under [scripts/](scripts/), corresponding tests under
[tests/](tests/), and relevant design or data documentation under
[doc/](doc/) or [data/](data/). See the directory guides for details.

## License

This project is distributed under the [MIT License](LICENSE).
