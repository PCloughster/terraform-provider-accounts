# terraform-provider-account

## Getting Started

This provider is available via the [Terraform Registry](https://registry.terraform.io/providers/ans-group/account/latest/docs) with Terraform v0.13+

> :warning: We strongly recommend pinning the provider version to a target major version, as to ensure future breaking changes do not affect workflows and automated CI pipelines

```
terraform {
  required_providers {
    account = {
      source  = "ans-group/account"
      version = "~> 1.0"
    }
  }
}

provider "account" {
  api_key = "abc"
}
```

## Getting Started (manual)

To get started, the `terraform-provider-account` binary (`.exe` extension if Windows) should be downloaded from [Releases](https://github.com/ans-group/terraform-provider-account/releases) and placed in the plugins directory (see [here](https://www.terraform.io/docs/configuration/providers.html#third-party-plugins) for more information). For this example, we'll place it in `~/.terraform.d/plugins/`

We'll then need to initialise terraform with our provider:

```console
terraform init
```

Finally, we can invoke `terraform apply` to apply our terraform configuration:

```console
terraform apply
```

## Documentation

Documentation is located within this repository at `/docs`, and is published in the [Terraform Registry](https://registry.terraform.io/providers/ans-group/account/latest/docs)

## Development

### Testing

Acceptance tests can be executed using `make` as below:

```
make testacc
```


### Releasing 

`goreleaser` is used to release the provider on Github. First, obtain your GPG fingerprint:

```
gpg -k
```

Cache GPG passphrase:

```
gpg --armor --detach-sign -n main.go
```

Finally tag and invoke `goreleaser`:

```
git tag v2.0.0
git push --tags
export GITHUB_TOKEN=<token>
export GPG_FINGERPRINT=<fingerprint>
export GPG_TTY=$(tty)
goreleaser --rm-dist
```
