PREREQUISITES:
Here,
1. we are provisioning aws services using Terraform.
2. Connecting them into a ci/cd pipeline
3. using iam + artifacts + stages.

The pipeline flow is
GitHub / CodeCommit
        ↓
    CodePipeline
        ↓
    CodeBuild
        ↓
 CodeDeploy / EC2
 
TERRAFORM
Terraform is an open-source infrastructure as code software tool
