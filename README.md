# Open Journals :: Deposit pull request

This action opens a pull request for an accepted paper and optionally merges it

## Usage

Usually this action is used as a step in a workflow after paper's branch including the needed files is created.

### Inputs

The action accepts the following inputs:

- **papers_repo**: Required. The repository containing the published and submitted papers in `owner/reponame` format.
- **issue_id**: Required. The issue number of the submission of the paper.
- **bot_token**: Required. The access token to be used to upload files, usually a bot account.
- **branch_prefix**: Optional. The prefix of the name of the paper's branch.
- **mode**: Optional. Valid values: [`dry-run`, `deposit`]. If `mode=deposit`, the PR will be merged and the topic branch deleted. Default: `dry-run`.

### Outputs

- **pr_url**: The URL for the created pull request

### Example

Use it adding it as a step in a workflow `.yml` file in your repo's `.github/workflows/` directory and passing your custom input values:

````yaml
on:
  workflow_dispatch:
   inputs:
      issue_id:
        description: 'The issue number of the submission'
jobs:
  processing:
    runs-on: ubuntu-latest
    steps:
      - name: Open Pull Request
        id: open-pr
        uses: xuanxu/deposit-pull-request-action@main
        with:
          papers_repo: myorg/myjournal-papers
          branch_prefix: myjournal
          issue_id: ${{ github.event.inputs.issue_id }}
          bot_token: ${{ secrets.BOT_ACCESS_TOKEN }}
          mode: dry-run
```
