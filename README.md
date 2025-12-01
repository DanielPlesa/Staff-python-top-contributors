## Top Python Contributors Scraper

This script ranks top Python contributors by exploring the most-starred repositories on GitHub, grabbing the top contributors from each project, and enriching every user with contribution stats, profile metadata, and a per-repo Python commit breakdown. Results are written to `sorted_top_python_contributors.csv`, sorted by total contributions.

## How It Works

- Pulls the top `REPO_LIMIT` Python repositories via the GitHub REST API.
- Harvests the top `CONTRIBUTORS_PER_REPO` contributors per repository.
- Uses the GitHub GraphQL API to collect names, locations, emails, profile URLs, yearly contribution totals, and Python commit summaries.
- Sorts everyone by total contributions and exports the final table to CSV.

## Requirements

- Python 3.9+ (any modern CPython works)
- GitHub personal access token (classic or fine-grained) with `public_repo` scope
- Python packages: `requests`

Install the Python dependency:

```bash
pip install requests
```

## Configuration

Open `github_contributors_last_year.py` and adjust the configuration block near the top:

- `GITHUB_TOKEN`: replace with your personal access token.
- `REPO_LIMIT`: how many top-starred Python repositories to scan (default 200).
- `CONTRIBUTORS_PER_REPO`: number of contributors to pull per repo (default 10).
- `OUTPUT_FILE`: destination CSV file name.

Keep your token secret—do not commit it.

## Running the Script

```bash
python github_contributors_last_year.py
```

The script prints progress as it iterates through repositories and users. Because it calls both the REST and GraphQL APIs heavily, it automatically sleeps when rate-limited; expect multi-minute runs for the default limits.

When the run finishes you will find the sorted results in `sorted_top_python_contributors.csv`.

## Tips


- Reuse the same output file to compare historical runs by checking git diffs against `sorted_top_python_contributors.csv`.

