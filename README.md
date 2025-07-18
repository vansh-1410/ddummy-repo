---

## ⚙️ How to Use This GitHub Action

1. Generate your **OpenAI API Key** from [https://platform.openai.com/account/api-keys](https://platform.openai.com/account/api-keys)
2. Go to your GitHub repo → **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret** → Add the following:
   - Name: `OPENAI_API_KEY`
   - Value: *your API key*

4. Add this workflow file in `.github/workflows/code-review.yml`:

```yaml
name: AI Code Reviewer

on:
  pull_request:
    types:
      - opened
      - synchronize

permissions: write-all

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@v3

      - name: AI Code Reviewer
        uses: vansh-1410/ai-code-reviewer@main
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
          OPENAI_API_MODEL: "gpt-4" # Optional
          exclude: "**/*.json, **/*.md" # Optional
