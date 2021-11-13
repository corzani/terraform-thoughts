# Terraform

## Best Practices

### Setup a "required_version" on "terraform" section

This would help to maintain the same state file avoiding different versions for different users.
The main idea would using the Terraform CLI on CI pipelines with different environment, avoiding users to apply changes directly without passing through the review (GIT pull request).

### Policy as a code (Sentinel module)

In big projects, where different areas of the architecture are handled by different team, additional checks might be required. Sentinel module does check policies correctness on a pull request, it's an additional layer before the human review.

### Code formatting

Terraform (and modules like Sentinel) does have a formatting tool in place.
It can be called using:

```sh
$ terraform fmt [options] [DIR]
```

Would an hook be usefult on a Git push?

### Remote backend

Terraform saves/updates state information whenever we apply changes. Those states are critical and should be stored in a safe remote place. Typically using services like AWS S3 with file versioning. Those states should be backed up.

```
provider "aws" {
    region     = "us-west-2"
    access_key = "my-access-key"
    secret_key = "my-secret-key"
}

terraform {
    required_version = "=x.y.z"

    backend "s3" {
        bucket = "mybucket"
        key    = "path/to/my/key"
        region = "us-east-1"
    }
}
```

### Variables

### Outputs