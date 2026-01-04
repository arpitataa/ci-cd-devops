# ci-cd-devops
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

When a developer pushes code to github, first the CodePipeline detects the change. Then the CodeBuild runs (build/test) and finally CodeDeploy deploys to EC2. Terraform's job is to create these services and wire them together.
