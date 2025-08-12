---
id: ut55aaqj40t85uwn3rdozge
title: aws_CICD_Testing
desc: ''
updated: 1753258180731
created: 1743570121943
---


- We need vscode , git , s3 , aws_code_commit , code_build and code_pipeline

1. Create repo in code_commit my_test
2. Create s3 bucket s3//my_test_bucket
3. Clone repo from code_commit

```bash
git clone https://git-codecommit.<region>.amazonaws.com/v1/repos/MyDemoRepo
cd MyDemoRepo

```

##  Add a sample application (app.py):

print("Hello from AWS CodePipeline!")

## add buildspec.yml
``` bash
version: 0.2  # Specifies the buildspec version

phases:
  install:
    runtime-versions:
      python: 3.9  # Defines the language runtime
  pre_build:
    commands:
      - echo "Installing dependencies..."
      - pip install -r requirements.txt  # If using Python
  build:
    commands:
      - echo "Building the application..."
      - python app.py  # Run your script
  post_build:
    commands:
      - echo "Build completed successfully."

artifacts:
  files:
    - '**/*'  # Upload all files to S3

```

 - Details

| Section    | Purpose                                                                 |
|------------|-------------------------------------------------------------------------|
| version    | Specifies the buildspec version (use 0.2)                               |
| phases     | Defines the steps CodeBuild follows (install, pre-build, build, post-build) |
| install    | Installs dependencies (e.g., Python, Node.js, Java, etc.)               |
| pre_build  | Prepares the environment (e.g., installing packages)                    |
| build      | Runs the actual build process                                          |
| post_build | Runs after the build (e.g., deploying, saving logs)                    |
| artifacts  | Specifies which files to save in S3                                    |

- git commit and push back to code-commit

## Create a CodeBuild Project
Go to AWS Console → CodeBuild.

Click Create build project.

Project name: MyDemoBuild.

Source provider: Select AWS CodeCommit → Choose MyDemoRepo.

Environment: Operating system: Amazon Linux 2

Runtime: Standard

Image: aws/codebuild/standard:5.0

Privileged: Unchecked

Buildspec:Select Use a buildspec file.

-----------------------------
## Create a CodePipeline

Source = Codecommit.

Build = CodeBuild

Dest = S3


