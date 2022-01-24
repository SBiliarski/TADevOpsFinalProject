# TADevOpsFinalProject
Sergei Biliarski's final project for Telerik Academy Upskill DevOps course 2021/2022.

The aim of this project is to showcase a basic CI/CD pipeline that first checks the app code for correct syntax and for vulnerabilities and then builds a simple web server in AWS using Terraform Infrastructure as Code. To demonstrate ChatOps, it reports its progress in a Slack channel using a webhook integration.


The GitHub action will connect to Terraform Cloud to execute the Terraform code. Terraform will generate a plan on every pull request and only apply it if the pull request is merged. The Terraform code creates and configures a security group and deploys an EC2 instance in AWS using a Ubuntu 12.04 LTS AMI. It configures a very basic Apache webserver with a single "Hello World" index.html using a "user_data" script. When Terraform is finished applying the plan it outputs the public web address of the web server.

![Diagram](Diagram.png)

The GitHub Actions workflow has 3 major steps - Terraform Basic Linter, SonarCloud and Terraform. Upon the successful completion of each step a message is sent to a Slack channel.


The Terraform Basic Linter workflow step will: 
- check Terraform code syntax by executing the Terraform-Lint GitHub Marketplace action: https://github.com/marketplace/actions/terraform-lint
- send a message to the Slack channel


The SonarCloud workflow step will:
- execute if previous step was successful
- send the code for Static Code Analysis to SonarQube using the SonarQube Scan acion: https://github.com/marketplace/actions/sonarqube-scan
- send a message to the Slack channel


The Terraform workflow step will:

- execute if previous step was successful
- check whether the configuration is formatted properly to demonstrate how you can enforce best practices
- generate a plan for every pull request
- apply the configuration when you update the main branch
- send a message to the Slack channel
