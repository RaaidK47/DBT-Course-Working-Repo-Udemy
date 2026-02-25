# Complete dbt Bootcamp - Student Working Repository

This repository is the working codebase for the Udemy course **"The Complete dbt (Data Build Tool) Bootcamp - Zero to Hero"**.

It includes:
- A dbt project in [`airbnb`](airbnb)
- Course references and setup material in [`_course_resources`](./_course_resources)
- A local Python environment managed with `uv`

## Tech Stack

- `dbt-core` `1.11.x`
- `dbt-snowflake` `1.11.x`
- `dbt-autofix`
- `dagster-dbt` and `dagster-webserver` (optional orchestration exploration)
- Python `>=3.10,<3.14`

## Repository Layout

```text
.
|-- airbnb/                 # Main dbt project
|   |-- models/             # src, dim, fct, mart models + docs/tests metadata
|   |-- tests/              # Singular + custom generic tests
|   |-- macros/             # Reusable Jinja macros
|   |-- snapshots/          # SCD snapshot configs
|   |-- seeds/              # Seed files (e.g., full moon dates)
|   |-- analyses/           # Ad-hoc analysis SQL
|   |-- dbt_project.yml
|   `-- packages.yml
|-- _course_resources/      # Course notes, setup SQL, example profile
|-- pyproject.toml          # Python dependencies (managed by uv)
`-- logs/                   # dbt logs/query logs
```

## Quick Start

1. Install dependencies:

```powershell
uv sync
```

2. Activate the virtual environment:

```powershell
.venv\Scripts\Activate.ps1
```

3. Configure your dbt profile (Snowflake credentials):
- Use [`_course_resources/EXAMPLE-profiles.yml`](./_course_resources/EXAMPLE-profiles.yml) as the template.
- Store your real profile at `~/.dbt/profiles.yml` (recommended), or use the local `airbnb/profiles.yml` for course convenience.
- Keep credentials and keys private.

4. Move into the dbt project directory:

```powershell
cd airbnb
```

5. Install dbt packages and validate connection:

```powershell
dbt deps
dbt debug
```

6. Run the project:

```powershell
dbt seed
dbt run
dbt test
```

## Useful dbt Commands

```powershell
# Build models + tests end-to-end
dbt build

# Full refresh incremental models
dbt run --full-refresh

# Source freshness checks
dbt source freshness

# Run a single model and its dependencies
dbt run --select mart_fullmoon_reviews

# Run tests for one model
dbt test --select dim_listings_w_hosts

# Generate and serve docs
dbt docs generate
dbt docs serve
```

## Course Resources

- Main course notes: [`_course_resources/course-resources.md`](./_course_resources/course-resources.md)
- Source dataset links: [`_course_resources/source-data-locations.md`](./_course_resources/source-data-locations.md)
- Class resources overview: [`_course_resources/README.md`](./_course_resources/README.md)

## Dev Container / Codespaces

This repo includes `.devcontainer` configuration for a ready-to-use development environment.  
The container runs `uv sync` automatically after creation.
