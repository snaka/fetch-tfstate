# fetch-tfstate

Fetch Terraform Cloud tfstate on GitHub Actions

**Warning: tfstate may contain information that should not be disclosed for security reasons, so do not use tfstate in public repositories by outputting its contents to logs, etc. This Action is intended for use in private repositories.**

## Usage

in your workflow yaml file

```yaml
jobs:
  example:
    runs-on: ubuntu-latest
    steps:
      - id: fetch-tfstate
        uses: snaka/fetch-tfstate@v1.0.0-beta.1
        with:
          terraform-cloud-token: ${{ secrets.TERRAFORM_CLOUD_TOKEN }}
          workspace: ${{ secrets.TF_WORKSPACE_ID }}
          path-to-tfstate: ${{ github.workspace }}/terraform.tfstate  # optional
      - show tfstate file
        run: echo ${{ steps.fetch-tfstate.outputs.path-to-tfstate }}
```

## Motivation

Deployment tools around ECS such as ecspresso and ecschedule can be conveniently used in conjunction with Terraform using tfstate.

However, if you are using Terraform Cloud and the repository that manages the terraform code is separated from the application code to be deployed, it is a little troublesome to get tfstate.

To solve this problem, this Action will download the latest tfstate of the specified workflow from Terraform Cloud on your behalf.
