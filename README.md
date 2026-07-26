# terraform-hcloud-certificate

> Managed or uploaded, the load balancer just needs the ID.

**Status:** 🚧 In development

## Overview

Terraform module that manages Hetzner Cloud certificates, both managed (Let's Encrypt, DNS-validated) and uploaded, exposing the certificate ID for load balancer services.

## Features

- One module for both `managed` and `uploaded` certificates, selected by a single `type` variable
- Managed certificates issued by Let's Encrypt over DNS validation, with the domain list as a plain variable
- Uploaded certificates take a PEM certificate and private key, read from files rather than inlined into state by hand
- Validation that a managed certificate has domains and an uploaded one has both PEM blocks, so a half-filled config fails at plan time
- Outputs the certificate ID, fingerprint and `not_valid_after`, so expiry is queryable from Terraform outputs
- Labels applied per certificate for renewal tracking and load balancer selectors

## Stack

Terraform + the hetznercloud/hcloud provider.

## Usage

```hcl
module "certificate" {
  source = "github.com/moveeeax/terraform-hcloud-certificate"

  name = "app-example-com"
  type = "managed"

  domain_names = [
    "app.example.com",
    "www.app.example.com",
  ]

  labels = {
    env = "prod"
  }
}
```

## License

MIT
