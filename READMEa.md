# Jenkins-practice

**Pipeline To call a specific directory inside a git repo**
pipeline {
agent any 
stages {
    stage('Git checkout(specific dir)') {
        steps {
            git branch: 'main', url: 'https://github.com/jyotisingh10061999/Terraform-9am-practice.git'
        }
    }
     stage('specific director') {
        steps {
            dir('Day-5-customNW') {
                // some block
            }
        }
    }
     stage('terraform init') {
        steps {
            sh 'terraform init'
            sh 'terraform plan'
        }
    }
}
}


<img width="682" height="612" alt="image" src="https://github.com/user-attachments/assets/4079d957-8810-45b6-8489-33b59c26d592" />



**Github action yaml file**

ame: Terraform Workflow

on: push: branches: - main

jobs: terraform: runs-on: ubuntu-latest

defaults:
  run:
    working-directory: Day-5-customNW

steps:
  - name: Checkout Code
    uses: actions/checkout@v4

  - name: Setup Terraform
    uses: hashicorp/setup-terraform@v3

  - name: Configure AWS Credentials
    uses: aws-actions/configure-aws-credentials@v4
    with:
      aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      aws-region: ap-south-1

  - name: Terraform Init
    run: terraform init

  - name: Terraform Plan
    run: terraform plan

    <img width="1406" height="603" alt="image" src="https://github.com/user-attachments/assets/863379b9-1004-4eb7-98b0-af6fff2862e3" />







