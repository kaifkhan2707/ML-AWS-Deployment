## Machine Learning Model Deployment on AWS
## Architecture

![Architecture Diagram](/images/Architecture.png)

**Detailed Implementation Plan:**

 1. **Project Setup & Infrastructure**

     - Initialize a repo with branches (main, dev, feature/*).
     - Enable branch protection rules (e.g., require PRs for main).
       
     **AWS EC2 Instance**
     - Launch an EC2 instance (e.g., t3.micro) in a private VPC.
       
     **Configure security groups to allow:**
     - SSH (port 22) from specific IPs.
     -  HTTPS (port 443) for application traffic.
     -  Install Docker and configure user data scripts for automation.
    
     **AWS ECR**
     -  Create an ECR repository (e.g., student-score-predictor).
     -  Configure lifecycle policies to prune old images.
   
     **IAM Roles**
     -  Create an IAM role for EC2 (ECSTaskExecutionRole) with permissions to:
     -  Access ECR (ecr:*, GetDownloadUrlForLayer).
     -  Write logs to CloudWatch (logs:PutLogEvents).
     -  Retrieve secrets from Secrets Manager (secretsmanager:GetSecretValue).

2. **CI/CD Pipeline**
     - Github Actions
   ![CI/CD Pipeline](/images/ML_CI_CD.PNG)
   ![CI Pipeline](/images/CI.PNG)
   ![CD Pipeline](/images/CD.PNG)

3. **Monitoring & Alerting**
    - Cloudwatch
   ![Cloudwatch](/images/cloudwatch.PNG)

4. **Model Training and Deployment**
   - Train the model using Jupyter notebooks or SageMaker.
     
     **Containerization**
   - Build a Docker image with Flask to serve predictions.
   - Include environment variables for model paths and secrets.
  
5. **Rollback Strategy**
   - Use ECR image tags (e.g., v1.0.0) to revert to previous versions.

    
