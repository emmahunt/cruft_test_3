# cruft_test_3

A dbt project.

Built on **snowflake** with dbt (`>=1.7,<2.0`), run on the dbt platform.
Maintained by emma.

## Getting started

This project runs on the dbt platform. The warehouse connection and credentials
are configured in the platform (connection + environments), so there is no
`profiles.yml` in this repo.

1. Connect this repository to your dbt platform project and configure the
   connection and a development environment in the platform UI.

2. Develop in dbt Studio, or locally with the dbt platform CLI:

   ```bash
   dbt deps           # install packages
   dbt build          # seed, run, and test everything
   ```

The project ships with example seeds (`raw_customers`, `raw_orders`) so it runs
end to end with no external warehouse data. Replace them with your real sources
as you build out the project.

## Project layout

```
seeds/      example raw data (replace with real sources)
models/
  staging/  one cleaned model per source table
  marts/    business-facing models built from staging
macros/     reusable SQL macros
snapshots/  slowly changing dimension snapshots
tests/      singular data tests
analyses/   ad-hoc analytical queries
```

## Continuous integration

CI runs as a dbt platform CI job triggered on pull requests — configure it in the
platform against your CI environment. The only GitHub Actions workflow in this
repo keeps the project in sync with its template (see below).

## Staying in sync with the template

This project was generated from a shared dbt template and is tracked with
[cruft](https://cruft.github.io/cruft/). When the template changes, pull the
updates in:

```bash
cruft check     # is this project behind the template?
cruft update    # apply template changes (review the diff before committing)
```

A scheduled GitHub Actions workflow (`.github/workflows/cruft-update.yml`) opens
a pull request automatically when the template moves ahead. The `cruft` pre-commit
hook also fails locally if the project drifts from the template.
