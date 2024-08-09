# CI-CD

CI/CD Pipeline for AWS ECS
Description
This project sets up a CI/CD pipeline using GitHub Actions to automate the deployment of a web application to AWS Elastic Container Service (ECS). The pipeline includes automated deployment, integration tests, and rollback functionality. It leverages Docker for containerization and Nginx as a reverse proxy.

Table of Contents
Installation
Configuration
Usage
Testing
Deployment
Rollback
Contributing
License
Installation
Follow these steps to set up the project locally:

Clone the Repository:

bash
Copy code
git clone https://github.com/saivijayy/CI-CD.git
cd CI-CD
Install Docker and AWS CLI

Follow the installation instructions provided here and here.

Install Node.js and npm (if required):

bash
Copy code
sudo apt update
sudo apt install -y nodejs npm
Configure AWS CLI:

bash
Copy code
aws configure
Enter your AWS credentials and default region.

Configuration
Set up GitHub Secrets:

Add the following secrets to your GitHub repository:

AWS_ACCESS_KEY_ID: Your AWS Access Key ID.
AWS_SECRET_ACCESS_KEY: Your AWS Secret Access Key.
ECS_CLUSTER: The name of your ECS cluster.
ECS_SERVICE: The name of your ECS service.
ECS_TASK_DEFINITION: The name of your ECS task definition.
Go to Settings > Secrets and variables > Actions in your GitHub repository and add these secrets.

Create and Configure task-definition.json:

Ensure that the task-definition.json file is correctly configured and located in the root directory of your repository. This file defines your ECS task configuration.

Usage
Run the CI/CD Pipeline:

The pipeline is triggered automatically on pushes to the main branch. To manually trigger it, use the GitHub Actions tab in your repository.

Local Development:

To run the application locally, follow these steps:

bash
Copy code
docker build -t my-app .
docker run -p 80:80 my-app
Access the application at http://localhost.

Testing
Run Integration Tests:

Integration tests are included in the CI/CD pipeline and are executed automatically during deployment.

Local Testing:

To run tests locally:

bash
Copy code
npm test
Ensure that all required test dependencies are installed.

Deployment
Deploy to AWS ECS:

The deployment process is automated through GitHub Actions. Ensure that your AWS credentials and ECS configuration are correctly set up in the GitHub Secrets.

The workflow file is located in .github/workflows/deploy.yml.

Monitor Deployment Logs:

View the deployment progress and logs from the GitHub Actions tab in your repository.

Rollback
Automatic Rollback:

The pipeline includes automatic rollback functionality. In case of deployment failure, the previous stable version will be redeployed automatically.

Manual Rollback:

To manually roll back, use the AWS CLI or AWS Management Console to update the ECS service with a previous task definition:

bash
Copy code
aws ecs update-service --cluster my-cluster --service my-service --task-definition previous-task-definition
Contributing
Fork the Repository:

Fork the repository and clone your fork.

Create a Feature Branch:

bash
Copy code
git checkout -b feature/your-feature
Make Changes and Commit:

bash
Copy code
git add .
git commit -m "Add your feature"
Push Changes and Create a Pull Request:

bash
Copy code
git push origin feature/your-feature
Open a pull request in the original repository.

Push commands for check
aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/k4n1g1v8
docker build -t check .
docker tag check:latest public.ecr.aws/k4n1g1v8/check:latest
docker push public.ecr.aws/k4n1g1v8/check:latest
