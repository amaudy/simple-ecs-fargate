# Simple ECS Cluster (Fargate)

Simple cluster for quick testing workload.

- Fargate launch type.
- AWS Load Balancer
- Terraform local state file.
- Use Nginx as example service

### Before run the script


copy `backend/dev.hcl.example` to `backend/dev.hcl` then edit to proper values.

```bash
rm -rf .terraform
terraform init -backend-config=./backend/dev.hcl
terraform plan -var-file="./tfvars/dev.tfvars" --out dev.plan
terraform apply "dev.plan"
```

Do the same for `staging` environment. Replace `dev` with `staging`


### Common CLI

List tasks

```
aws --region us-east-1 ecs list-tasks --cluster my-cluster
```

example output

```
{
    "taskArns": [
        "arn:aws:ecs:us-east-1:xxxxxxxx:task/my-cluster/0bff5882753d4bb69798bb62bec2e1e0",
        "arn:aws:ecs:us-east-1:xxxxxxxx:task/my-cluster/8da81093d91a4ad888459226c44c5086",
        "arn:aws:ecs:us-east-1:xxxxxxxx:task/my-cluster/fef9f0ba0da6419bb366e2c095a1ece5"
    ]
}
```
Describe the tasks

```bash
aws --region us-east-1 ecs describe-tasks --cluster my-cluster --tasks arn:aws:ecs:us-east-1:xxxxxxxx:task/my-cluster/0bff5882753d4bb69798bb62bec2e1e0
```
