# GCP Cloud Storage Bucket — Terraform

This module creates a Google Cloud Storage (GCS) bucket with configurable options for storage class, versioning, lifecycle rules, and more.

## Usage

```hcl
module "bucket" {
  source = "./"

  project_id   = "my-gcp-project"
  bucket_name  = "my-unique-bucket-name"
  location     = "US"
  storage_class = "STANDARD"

  versioning_enabled          = true
  uniform_bucket_level_access = true

  lifecycle_rules = [
    {
      action_type   = "Delete"
      condition_age = 365
    }
  ]

  labels = {
    environment = "dev"
    managed_by  = "terraform"
  }
}
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|----------|
| `project_id` | The GCP project ID | `string` | — | yes |
| `region` | The GCP region | `string` | `"us-central1"` | no |
| `bucket_name` | The name of the GCS bucket (must be globally unique) | `string` | — | yes |
| `storage_class` | The storage class of the bucket | `string` | `"STANDARD"` | no |
| `location` | The location of the bucket | `string` | `"US"` | no |
| `force_destroy` | Allow Terraform to delete the bucket even if it contains objects | `bool` | `false` | no |
| `uniform_bucket_level_access` | Enable uniform bucket-level access | `bool` | `true` | no |
| `versioning_enabled` | Enable object versioning | `bool` | `false` | no |
| `lifecycle_rules` | List of lifecycle rules | `list(object)` | `[]` | no |
| `labels` | Labels to apply to the bucket | `map(string)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| `bucket_name` | The name of the bucket |
| `bucket_url` | The base URL of the bucket (`gs://<bucket-name>`) |
| `bucket_self_link` | The URI of the bucket |
