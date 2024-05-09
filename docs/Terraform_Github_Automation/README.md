
# Terraform Github Repository Automation

In this section we will cover the documentation about repository automation
modules we have.

Shortly, the repository called "terraform-automation" from Digital Anthropic
github contain all modules necesary for repository creation and also branch
protection settings of that repository.

The repository "terraform-automation" is linked with a terraform cloud
workspace. Which means that if you ever wanna create a repository inside github
orgationation you can automate the creation using this repository.

## How to use

To create a new repository you need to use `local.tf` file located in the root
of the repository. Below is an example of how to use it.

```hcl
locals {
  repos = {
    "terraform-in-mkdocs" = {
      description        = ""
      gitignore_template = "Terraform"
      name               = "terraform-in-mkdocs"
      topics             = ["mkdocs", "terraform"]
      visibility         = "private"
    }

    "terraform-automation" = {
      description        = ""
      gitignore_template = "Terraform"
      name               = "terraform-automation"
      topics             = ["mkdocs", "terraform"]
      visibility         = "private"
    }

    "terraform-aws-cloudfront" = {
      description        = ""
      gitignore_template = "Terraform"
      name               = "terraform-aws-cloudfront"
      topics             = ["mkdocs", "terraform"]
      visibility         = "public"
    }

    "terraform-modules" = {
      description        = ""
      gitignore_template = "Terraform"
      name               = "terrafrom-modules"
      topics             = ["mkdocs", "terraform"]
      visibility         = "private"
    }

    "new-repo-name" = {
      description        = ""
      gitignore_template = "Terraform"
      name               = "new-repo-name"
      topics             = ["mkdocs", "terraform"]
      visibility         = "private"
    }
  }
}
```

Change the "new-repo-name" object with the one you want. You can also add a
description of the repo, a gitignore template, topics of the repo and the
visibility(public/private).

*Note*: You will need to create a new branch and merge your changes into main,
because of branch protection rules.

After you will have a Pull Request ongoing on github with your changes terraform
will start a pipeline for planing part. Note that will be only planning without
apply.

If the plan will be a success you can merge your branch into main. Another
pipeline will be started by terraform with the same plan but now you will be
able to apply the plan. If the apply is also a success you can now watch the
your brand new repo in Digital Anthropic ORG.

*Note*: You can add how many repos you need.

## Resources

| Name | Type |
|------|------|
| [github_branch_protection.self](https://registry.terraform.io/providers/integrations/github/6.0.0/docs/resources/branch_protection) | resource |
| [github_repository.self](https://registry.terraform.io/providers/integrations/github/6.0.0/docs/resources/repository) | resource |
| [github_team_repository.self](https://registry.terraform.io/providers/integrations/github/6.0.0/docs/resources/team_repository) | resource |
