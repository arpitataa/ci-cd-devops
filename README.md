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

WHAT IS A CI/CD PIPELINE? 
Imagine an automatic system that does this

“When I push code to GitHub, AWS should automatically build it and deploy it.”

This automatic system is called a CI/CD pipeline.

What is Terraform?

Terraform is a tool that creates AWS services automatically using code. Instead of clicking in AWS Console, we write files and terraform reads them and AWS resources are created.

What is a S3 Bucket? 

S3 is just a storage box in AWS.

Why S3?

When the pipeline runs:
Source code is zipped
Build output is zipped and these ZIP files must be stored somewhere and that place is S3.

We create 1 S3 bucket and CodePipeline uses it automatically. We think “Pipeline needs a bag to carry files → S3”.

What is IAM?

IAM controls who can do what in AWS.

Why IAM roles?

AWS services cannot do anything by default. So we must specify:
CodePipeline → allowed to use S3, CodeBuild, CodeDeploy
CodeBuild → allowed to write logs and read artifacts
CodeDeploy → allowed to deploy to EC2

Example:
1. Source Stage Artifact
Contains: your GitHub repo files
Stored as: ZIP in S3

2. Build Stage Artifact
Contains: compiled / tested output
Stored as: ZIP in S3

3. Deploy Stage
Takes artifact from S3
Deploys it to EC2

What is the source stage?

This is where your pipeline gets your code from.
Options:
GitHub (easy)
CodeCommit (AWS Git)

What happens?
You push code.
Pipeline detcts change.
Pipeline starts running.
