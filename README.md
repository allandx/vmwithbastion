# Terraform

Terraform scripts that I use to provision my servers with jumphost (for testing purposes)

## Quickstart

To create the infra

```bash
cd aws
terraform init
# May require additional information such as Google Cloud Project ID
terraform plan -out initial.plan
# Applying plan
terraform apply initial.plan
```

To destroy it

```bash
cd aws
terraform init
# May require additional information such as Google Cloud Project ID
terraform plan -out destroy.plan -destroy
# Applying plan
terraform apply destroy.plan
```

## Tripped problems

- Enabling/disabling certain components to be provisioned. Some blogs were mentioning of using `count` field and setting it to 0 to "disable it" and 1 to "enable it". Also, needed to create a range of servers based on some instance number - so hence, the following:

```
│ Error: Invalid combination of "count" and "for_each"
│ 
│   on main.tf line 180, in resource "google_compute_instance" "etcd":
│  180:   for_each = range(1,3,1)
│ 
│ The "count" and "for_each" meta-arguments are mutually-exclusive, only one should be used to be explicit about the number of
│ resources to be created.
```

## Useful references

- https://spacelift.io/blog/terraform-best-practices
- Use import for getting stuff that has been deployed before into terraform. Tweak it till nothing is "changed" before it's managed by terraform. https://spacelift.io/blog/importing-exisiting-infrastructure-into-terraform
- Use `replace` flag if servers need to replace due to bad updates etc