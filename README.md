# Advanced Computing Center User Guide

## Description

This repository contains documentation for the users of the [**Advanced Computing Center** (ACC)](https://edis.unibuc.ro/data-center-si-laboratoare-de-acces/) of the [University of Bucharest](https://unibuc.ro/?lang=en).

## Contributing instructions

We use [MkDocs](https://www.mkdocs.org/) for generating the documentation from [Markdown](https://en.wikipedia.org/wiki/Markdown) source files. We recommend using [uv](https://docs.astral.sh/uv/) for handling your [Python](https://www.python.org/) install and virtual environment.

Use `uv sync` to install the required packages, then start a local development server by running
```shell
uv run mkdocs serve
```
The built docs will be available at `https://localhost:8000`.
