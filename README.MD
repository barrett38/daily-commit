# Multiple Daily Commits

This GitHub Actions workflow performs automated commits to the repository every 3 hours. It updates a file named `multiple-daily-updates.txt` with the current date and time, commits the change, and pushes it to the repository.

## Usage

To use this workflow, simply copy the `daily-commit.yml` file into the `.github/workflows` directory of your repository.

## Configuration

1. Ensure you have a `.github/workflows` directory in your repository.
2. Copy the `daily-commit.yml` file into the `.github/workflows` directory.
3. The `GITHUB_TOKEN` is automatically provided by GitHub Actions, so you do not need to manually set it up in your repository secrets.
4.

## Example

Here is the content of the `daily-commit.yml` file:

```yaml
name: Multiple Daily Commits

on:
  schedule:
    - cron: "0 */3 * * *" # This runs every 3 hours

jobs:
  daily-commit:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: "14"

      - name: Make a Change
        run: |
          echo "Update: $(date)" >> multiple-daily-updates.txt

      - name: Commit Changes
        # Replace the username and email field below
        # with correct GitHub Email and Username
        run: |
          git config --global user.name "barrett38"
          git config --global user.email "barrett1614@gmail.com"
          git add multiple-daily-updates.txt
          git commit -m "Update: $(date)"
          git push
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          # This token is provided by GitHub Actions
          # and does not need to be replaced with any other value
```
