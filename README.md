# terraform-aws-oidc

## Overview

The `terraform-aws-oidc` module provides a simple way to create OpenID Connect (OIDC) providers in AWS using Terraform. This module is designed to help you manage multiple OIDC providers efficiently while maintaining a clean and modular infrastructure setup.

## Features

- Create OIDC providers in AWS.
- Support for multiple OIDC providers for different AWS accounts.
- Easy to integrate with existing Terraform modules.
- Well-structured for modular and reusable configurations.

## Requirements

- Terraform 0.12 or higher
- AWS provider 3.0 or higher

## Usage

To use this module, include the following in your Terraform configuration:

```hcl

variable "oidc_providers" {
  type = map(list(object({
    idp_url    = string
    audience    = list(string)
    thumbprint  = optional(list(string), ["123456"])
    workspace   = string
  })))
  default = {
    "account1" = [
       {
         idp_url   = "https://api.bitbucket.org/2.0/workspaces/example/pipelines-config/identity/oidc"
         audience  = ["ari:cloud:bitbucket::workspace/example-audience"]
         workspace = "example"
       },
      {
         idp_url   = "https://api.bitbucket.org/2.0/workspaces/example2/pipelines-config/identity/oidc"
         audience  = ["ari:cloud:bitbucket::workspace/example-audience2"]
         workspace = "example2"
      }
    ],
    "account2" = [
      {
         idp_url   = "https://api.bitbucket.org/2.0/workspaces/example3/pipelines-config/identity/oidc"
         audience  = ["ari:cloud:bitbucket::workspace/example-audience3"]
         workspace = "example3"
      }
    ]
  }
}

```

