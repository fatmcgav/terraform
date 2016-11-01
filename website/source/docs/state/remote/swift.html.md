---
layout: "remotestate"
page_title: "Remote State Backend: swift"
sidebar_current: "docs-state-remote-swift"
description: |-
  Terraform can store the state remotely, making it easier to version and work with in a team.
---

# swift

Stores the state as an artifact in [Swift](http://docs.openstack.org/developer/swift/).

-> **Note:** Passing credentials directly via configuration options will
make them included in cleartext inside the persisted state. Use of
environment variables.

## Example Usage

```
terraform remote config \
	-backend=swift \
	-backend-config="path=terraform_state"
```

## Example Referencing

```
data "terraform_remote_state" "foo" {
	backend = "swift"
	config {
		path = "terraform_state"
	}
}
```

## Configuration variables

The following configuration options are supported:

 * `auth_url` / `OS_AUTH_URL` (Required) - The Identity authentication URL.
 * `path` - (Required) The path where to store `terraform.tfstate`.
 * `user_name` / `OS_USERNAME` (Required) - Username to login with.
 * `user_id` - (Optional) The User ID to login with. If omitted, the
   `OS_USER_ID` environment variable is used.
 * `password` / `OS_PASSWORD` (Required) - Password to login with.
 * `region_name` / `OS_REGION_NAME` (Required) - The region in which to store `terraform.tfstate`.
 * `tenant_id` / `OS_TENANT_ID` (Optional) The ID of the Tenant (Identity v2) or Project
  (Identity v3) to login with. If omitted, the `OS_TENANT_ID` or
  `OS_PROJECT_ID` environment variables are used.
 * `tenant_name` / `OS_TENANT_NAME` (Required) - The Name of the Tenant (Identity v2)
  or Project (Identity v3) to login with. If omitted, the `OS_TENANT_NAME` or
  `OS_PROJECT_NAME` environment variable are used.
 * `domain_id` - (Optional) The ID of the Domain to scope to (Identity v3). If
   If omitted, the following environment variables are checked (in this order):
   `OS_USER_DOMAIN_ID`, `OS_PROJECT_DOMAIN_ID`, `OS_DOMAIN_ID`.
 * `domain_name` / `OS_DOMAIN_NAME` (Optional) - The Name of the Domain to scope to
 (Identity v3). If omitted, the following environment variables are checked (in this
  order): `OS_USER_DOMAIN_NAME`, `OS_PROJECT_DOMAIN_NAME`, `OS_DOMAIN_NAME`,
  `DEFAULT_DOMAIN`.
 * `insecure` / `OS_INSECURE` - (Optional) Trust self-signed SSL certificates. If
  omitted, defaults to false.
