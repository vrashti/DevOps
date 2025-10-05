Here are Topics wise Interview Questions:
1. AWS
    1. 1. AWS Fundamentals

What is AWS and what are its core services?

Explain the difference between Regions and Availability Zones.

What are edge locations in AWS?

What is the Shared Responsibility Model in AWS?

How does AWS ensure high availability and fault tolerance?

What’s the difference between scalability and elasticity?

What are IAM roles and policies?

What is the difference between IAM User, Group, and Role?

How do you securely manage AWS access credentials?

How can you implement the principle of least privilege in AWS IAM?

    1. 2. Compute (EC2, Auto Scaling, Load Balancing)

What is an EC2 instance?

What types of EC2 instances have you used?

Explain On-Demand, Reserved, and Spot Instances.

What is an AMI and how do you create one?

What is a Security Group?

What is the difference between a Security Group and a Network ACL?

How do you connect to an EC2 instance?

What are EC2 user data and metadata?

What is Auto Scaling and how does it work?

How do you configure an Application Load Balancer?

What’s the difference between ALB, NLB, and CLB?

How would you troubleshoot an EC2 instance not accessible via SSH?

What is Elastic IP and when should you use it?

How can you attach and detach EBS volumes from EC2 instances?

What’s the difference between EBS and Instance Store volumes?

3. Storage (S3, EBS, EFS, Glacier)

What is Amazon S3?

Explain S3 bucket policies and ACLs.

How do you secure an S3 bucket?

What are S3 storage classes?

What is S3 versioning and when should you enable it?

What is S3 lifecycle management?

What is S3 Transfer Acceleration?

What is the difference between S3 and EFS?

What’s the difference between EBS and EFS?

What is Glacier used for?

4. Networking (VPC, Route 53, etc.)

What is a VPC?

Explain the components of a VPC.

What is the difference between a public and private subnet?

What is an Internet Gateway?

What is a NAT Gateway and why is it used?

What are route tables in AWS?

How do you connect two VPCs together?

What is a VPC Peering connection?

What is a VPC Endpoint?

What is Route 53?

Explain routing policies in Route 53.

What is a hosted zone?

How do you register a domain in AWS?

What is an Elastic Network Interface (ENI)?

How do you troubleshoot a VPC network connectivity issue?

5. Databases

What is Amazon RDS?

What are RDS Read Replicas?

What is Multi-AZ deployment in RDS?

What is DynamoDB and when would you use it?

What is Amazon Aurora?

How do you take database backups in AWS?

What’s the difference between RDS automated backups and snapshots?

How do you improve database performance in AWS?

How do you secure RDS instances?

What is Amazon ElastiCache used for?

6. DevOps & CI/CD on AWS

What AWS services are used for CI/CD?

What is AWS CodePipeline?

What is CodeBuild used for?

What is CodeDeploy and how does it work?

How do you integrate Jenkins with AWS?

How can you store build artifacts in AWS?

How can you trigger a CodePipeline automatically?

How do you roll back a deployment in AWS?

What are Blue-Green deployments in AWS?

How do you store secrets for pipelines in AWS?

7. Infrastructure as Code

What is AWS CloudFormation?

What are CloudFormation stacks and templates?

What’s the difference between CloudFormation and Terraform?

What are parameters and outputs in CloudFormation?

How do you manage dependencies in CloudFormation?

How can you update an existing CloudFormation stack safely?

What is Drift Detection in CloudFormation?

What’s the difference between declarative and imperative IaC?

How do you handle secrets in Terraform when using AWS?

What is AWS CDK and how does it differ from CloudFormation?

8. Containers & Serverless

What is Amazon ECS?

What is EKS?

What’s the difference between ECS and EKS?

How do you deploy a Docker container on ECS?

What is Fargate and when should you use it?

What is AWS Lambda?

What are the limits of AWS Lambda?

How do you monitor and debug Lambda functions?

How can you secure environment variables in Lambda?

What’s the difference between Lambda and EC2 for hosting apps?

9. Monitoring & Logging

What is Amazon CloudWatch used for?

What are CloudWatch Alarms?

What is CloudWatch Logs Insights?

How do you monitor EC2 or RDS using CloudWatch?

What is AWS CloudTrail?

What’s the difference between CloudWatch and CloudTrail?

How do you create custom CloudWatch metrics?

What is AWS Config used for?

How can you set up alerting for high CPU utilization on EC2?

How do you centralize logs in AWS from multiple services?



AWS Core & Infrastructure – Scenario-Based Q&A (Set 1)
1. Your EC2 instance suddenly became unreachable via SSH. What steps do you take?

Check if the Security Group allows inbound SSH (port 22) and the instance is in the running state. Then, verify the key pair and network ACLs. If still blocked, use EC2 Serial Console or System Logs from the console to debug network misconfiguration or OS-level firewall rules.

2. How do you handle an S3 bucket showing "Access Denied" even with the right IAM permissions?

It usually occurs when S3 Block Public Access is enabled or a Bucket Policy explicitly denies access. I check both the IAM policy and the bucket policy JSON for conflicts and confirm the object-level ACLs aren’t overriding access.

3. Your EC2 application is throwing “Disk full” errors. How do you resolve it without downtime?

I use df -h to confirm usage, clean unnecessary logs, and then increase the EBS volume size via AWS Console. After resizing, I run sudo growpart and resize2fs inside the instance to expand the filesystem without stopping it.

4. You notice your EC2 instance is restarting automatically. What’s the root cause?

Check CloudWatch metrics and System Logs. If there are “system-reboot” or “instance-reboot” messages, it could be AWS hardware maintenance. For software-related restarts, inspect /var/log/messages and auto-update scripts or cron jobs.

5. You deployed a web app on EC2, but it’s not reachable on port 8080. What’s your approach?

Confirm app is listening with netstat -tulnp | grep 8080, then check Security Group and Network ACL for port 8080. Also ensure the application is bound to 0.0.0.0, not just localhost, and verify EC2 public IP or Load Balancer DNS access.

6. How do you automate daily S3 backups from EC2?

I use a cron job running AWS CLI commands like aws s3 sync /data s3://my-backups/ --delete, or configure an S3 lifecycle policy. For larger setups, I use AWS Backup or automation via Lambda + CloudWatch Events.

7. A user accidentally deleted an S3 object. Can you restore it?

If Versioning was enabled, I can easily restore it by retrieving the previous version using AWS CLI. If not, I check if S3 Cross-Region Replication or Backup was enabled; otherwise, it’s permanently lost.

8. Your team complains of slow performance accessing S3 objects. How do you optimize it?

I enable S3 Transfer Acceleration, use CloudFront caching, or ensure data is accessed from the closest AWS region. I also review request patterns and move frequently accessed data to S3 Intelligent-Tiering.

9. How do you secure sensitive credentials in AWS?

I use AWS Secrets Manager or SSM Parameter Store (SecureString) to store credentials, then access them in pipelines or EC2 using IAM roles instead of embedding them in code.

10. You need to give temporary AWS console access to a developer. How do you manage that?

I create an IAM Role or temporary user with an IAM policy scoped to least privilege. Then, use STS (Security Token Service) to generate temporary credentials that expire after a few hours.

11. How do you restrict access to an S3 bucket to only an EC2 instance?

Attach an IAM Role to the EC2 instance with permissions for that specific bucket and update the Bucket Policy with a condition "Principal": { "AWS": "arn:aws:iam::<account-id>:role/<role-name>" }".

12. Your EC2 instance’s CPU utilization is constantly 100%. How do you fix this?

I use CloudWatch metrics to confirm CPU spikes, then check running processes using top. Based on load, I either scale vertically (bigger instance) or horizontally via Auto Scaling Group.

13. You need to allow your private EC2 instance to access the internet. How do you do it?

I attach a NAT Gateway in a public subnet and update the route table for the private subnet to direct internet-bound traffic to the NAT. This ensures outbound access without making the instance public.

13. You need to allow your private EC2 instance to access the internet. How do you do it?

I attach a NAT Gateway in a public subnet and update the route table for the private subnet to direct internet-bound traffic to the NAT. This ensures outbound access without making the instance public.

14. What’s your approach to managing AWS credentials in CI/CD pipelines?

I never store AWS keys directly in Jenkins or GitHub. I configure IAM Roles for Service Accounts (IRSA) in EKS, or Jenkins credentials plugin with AWS CLI profile, or use OIDC-based role assumption for secure access.

15. How do you monitor EC2 instance health automatically?

I enable EC2 Status Checks and configure CloudWatch Alarms to trigger SNS notifications or Lambda functions for automated recovery. Also, I use AWS Systems Manager Agent (SSM) for periodic health checks.

16. You need to connect two VPCs for communication. What are your options?

I can use VPC Peering for direct communication, or Transit Gateway if multiple VPCs need interconnectivity. For hybrid setups, I use VPN or Direct Connect.

17. How do you detect and block unusual traffic patterns to your EC2 instance?

Use AWS GuardDuty for anomaly detection, CloudWatch metrics, and WAF (Web Application Firewall) for protection. I also review VPC Flow Logs to identify IPs or patterns and block them in Security Groups.

18. What’s your strategy for logging and auditing user activity in AWS?

Enable AWS CloudTrail in all regions and configure it to send logs to an S3 bucket. Then, integrate it with CloudWatch Logs Insights or Athena for analysis of API activity and anomalies.

19. How do you handle cost optimization for EC2 instances?

I monitor usage with AWS Cost Explorer and Compute Optimizer. Then, I right-size instances, use Reserved Instances or Savings Plans, and schedule non-production instances to stop automatically at night using Lambda + EventBridge.

20. You deployed an app in a VPC but it can’t connect to RDS. What do you check first?

I verify the RDS instance’s subnet and security group allow inbound traffic from the EC2’s private IP. Both should be in the same VPC or peered VPC, and the DB endpoint should be used (not public IP).


Set 2 — CI/CD, Jenkins, Terraform, and Ansible

1. Your Jenkins pipeline fails after a code commit. How do you debug it?

I start by checking the console output in Jenkins. If it’s a build failure, I verify Maven/Gradle logs; if it’s a pipeline script issue, I review the Jenkinsfile syntax. For environment issues, I ensure the agent has correct dependencies and AWS credentials.

2. Jenkins shows “Permission denied” while deploying to EC2. What’s your fix?

It usually happens when .pem file permissions are too open or the key path is wrong. I run chmod 400 key.pem and ensure the pipeline user has access to that file. Also, I verify that the EC2 user (ubuntu/ec2-user) is correct in the scp or ssh step.

3. Your Jenkins job runs successfully but the deployment isn’t visible on EC2. What do you check?

I confirm the artifact path in Jenkins (target/*.jar), ensure it’s copied to the right EC2 directory, and verify the application is started using ps -ef | grep java. If using PM2/systemd, I check service logs for startup errors.

4. How do you securely handle AWS credentials in Jenkins?

I use Jenkins Credentials plugin and store AWS Access/Secret Keys or better — assign IAM Roles to EC2/Jenkins agents. Then, in pipeline steps, I use withAWS(credentials: 'aws-creds') or the awscli profile.

5. You need to automate EC2 provisioning. How do you achieve that with Terraform?

I define EC2 resources in .tf files (AMI, key, SG, etc.), initialize Terraform using terraform init, plan the deployment with terraform plan, and create it using terraform apply. I store the state file in S3 for team collaboration.

6. Terraform apply fails saying “Resource already exists.” What do you do?

That means Terraform state is out of sync with real AWS resources. I either import the resource using terraform import, or manually remove it from state with terraform state rm before applying again.

7. How do you manage multiple environments (dev, test, prod) in Terraform?

I use workspaces (terraform workspace new dev) or separate state files and variable files for each environment. It keeps resource configurations isolated and prevents accidental cross-environment changes.

8. Your Terraform variable file contains secrets. How do you secure them?

I move them to AWS Secrets Manager, SSM Parameter Store, or .tfvars files excluded via .gitignore. In CI/CD, I inject secrets dynamically through environment variables.

9. How do you roll back a failed Terraform deployment?

Terraform doesn’t have native rollback — so I use versioned modules and Git tags to revert to a previous configuration, followed by terraform apply. I also take snapshots of RDS or EBS volumes before major infra changes.

10. You need to configure Nginx on 5 EC2 servers. How do you automate that?

I write an Ansible playbook with a yum or apt module to install Nginx, a copy module to deploy config files, and service to start it. I run it using ansible-playbook nginx.yml -i inventory.

11. Ansible playbook fails at one task but you want to continue others. How do you handle that?

I add ignore_errors: yes for non-critical tasks or use block with rescue to handle errors gracefully. This helps in long playbooks where some tasks can fail without breaking the entire run.

12. You get “UNREACHABLE” error in Ansible for certain hosts. How do you fix it?

It usually means SSH connectivity is broken. I check if the target EC2 is reachable via ping/SSH, and verify inventory IPs, private key path, and ansible_user (ubuntu/ec2-user) are correct.

13. How do you integrate Jenkins with GitHub for CI/CD triggers?

I configure a GitHub Webhook pointing to Jenkins URL (/github-webhook/), and enable GitHub plugin in Jenkins. Then, in the job, I select “GitHub hook trigger for GITScm polling” so that every push triggers a build.

14. How do you manage Jenkins configuration backups?

I back up /var/lib/jenkins/ (especially jobs/ and config.xml) using a cron-based S3 sync job. For advanced setups, I use Jenkins Configuration as Code (JCasC) to version control job definitions in YAML.

15. Jenkins agent is offline. What’s your debugging process?

I check the agent log under “Manage Nodes” → “Logs”. Usually, it’s a network issue, Java version mismatch, or authentication token expired. Restarting the agent service and verifying java -version often resolves it.

16. Your Jenkins job takes too long to build. How do you optimize it?

I enable parallel stages, use Docker agents for lightweight builds, cache Maven dependencies, and offload heavy builds to EC2 spot instances. I also move repetitive setup commands into shared pipeline libraries.

17. How do you deploy a new microservice to AWS using CI/CD?

Code push triggers Jenkins → builds Docker image → pushes it to ECR → updates ECS service or EKS deployment using AWS CLI/Terraform. Rollback handled by previous task version in ECS/EKS.

18. Terraform plan shows resource recreation even though nothing changed. Why?

That happens when non-deterministic attributes (like tags or timestamps) change or providers drift. I review diffs, and if it’s cosmetic, I use lifecycle { ignore_changes = [attribute] } to avoid recreation.

19. How do you ensure zero-downtime deployment for an EC2-hosted app via Jenkins?

I use Blue-Green Deployment — launch a new EC2 with the new version, health-check it, then switch the Elastic IP or Load Balancer target group to the new instance. Old one is terminated after validation.

20. How do you troubleshoot when an Ansible playbook changes unexpectedly modify resources?

I first run the playbook in check mode (--check) to preview changes. Then, use tags and handlers to control task execution. If changes are unintended, I validate variables and inventory consistency.


Set 3 — Docker, Kubernetes, and AWS EKS

1. Your Docker container exits immediately after starting. How do you troubleshoot it?

I check the container logs using docker logs <container_id>. If it’s due to a missing foreground process, I make sure the main app command (like CMD ["java", "-jar", "app.jar"]) runs continuously. For debugging, I start it with docker run -it --entrypoint /bin/bash to inspect manually.

2. Docker build fails due to permission denied on copying files. What’s the fix?

This usually happens because of incorrect context or permissions. I check the .dockerignore and ensure files exist in the build context. I also use USER root temporarily or RUN chmod to adjust permissions inside the image.

3. How do you reduce Docker image size?

I use multi-stage builds, choose lightweight base images (like alpine), clean up temporary files with rm -rf /var/lib/apt/lists/*, and combine layers to reduce overhead. This helps in faster deployments and smaller storage costs.

4. You pushed a wrong image tag to Docker Hub. How do you fix it?

I delete or deprecate the wrong tag using the Docker Hub UI or API, rebuild the correct version with the right tag (docker build -t user/app:v2 .), and push it again. I also update CI/CD to automate proper tagging using Git commit hashes.

5. Your application inside a Docker container can’t connect to a database. What do you check?

I verify network connectivity between containers using docker network ls and docker inspect. Then check DB hostname and port mapping. If using Docker Compose, I use service names instead of localhost (DB_HOST=db).

6. How do you handle secrets in Docker containers?

Never store secrets in the image. I use environment variables, Docker secrets, or AWS SSM Parameter Store. In production, Kubernetes secrets are a better approach since they encrypt and manage sensitive values.

7. Kubernetes Pod stuck in CrashLoopBackOff — what’s your debugging approach?

I check pod logs (kubectl logs pod-name), describe the pod (kubectl describe pod), and look for events. Often it’s wrong config, missing env vars, or app startup failure. I fix the config or run the container interactively to debug.

8. You deployed a new version in Kubernetes but users still see the old one. Why?

That usually happens when the old pods are still running or the Service is caching endpoints. I check rollout status with kubectl rollout status deployment/<app> and verify if the image tag was updated properly.

9. How do you perform a rolling update in Kubernetes?

I update the deployment image tag (kubectl set image deployment/app app=image:v2), which triggers a rolling update automatically. Kubernetes handles pod termination and startup gracefully, ensuring zero downtime.

10. You need to access a pod running in private subnet EKS. How do you do it?

I use kubectl port-forward, bastion host, or expose temporarily via LoadBalancer Service (only for testing). For secure access, I connect via AWS SSM Session Manager or a VPN to VPC.

11. How do you debug when pods are not scheduling on nodes?

I run kubectl describe node and check taints, resource requests, or affinity rules. If nodes show NotReady, I check kubelet logs or EC2 instance health. Often, scaling the cluster or adjusting limits fixes it.

12. Your EKS cluster costs are high. How do you optimize them?

I enable Cluster Autoscaler, use Spot Instances for worker nodes, and optimize pod requests/limits. I also offload static content to S3 and stop unused dev clusters during non-business hours.

13. A pod needs access to S3 but you don’t want to use keys. What do you do?

I use IAM Roles for Service Accounts (IRSA) in EKS, which allows pods to assume IAM roles directly. This avoids embedding AWS credentials inside containers — improving both security and compliance.

14. How do you monitor Kubernetes cluster health?

I use Prometheus + Grafana for metrics, Kubernetes Dashboard for visualization, and kubectl top nodes/pods for resource usage. Cloud-native options like AWS CloudWatch Container Insights also help track performance.

15. Kubernetes pod cannot pull image from ECR. How do you fix it?

The EKS nodes need the proper IAM role with ECR permissions. I verify credentials with aws ecr get-login-password. Sometimes, image pull secrets must be created if using private repos (kubectl create secret docker-registry).

16. Your Kubernetes config update doesn’t reflect in pods. Why?

ConfigMaps and Secrets don’t auto-refresh. I either restart the pods or use annotations with timestamps to trigger redeployment. Tools like Reloader can automate this.

17. How do you handle scaling in Kubernetes?

I use Horizontal Pod Autoscaler (HPA) based on CPU/memory metrics and Cluster Autoscaler for node scaling. For custom scaling logic, I integrate Prometheus metrics or external triggers (e.g., SQS queue length).

18. You need to deploy multiple microservices with common configurations. How do you manage it?

I use Helm charts — define templates for deployments, services, and configs. Each microservice just overrides values in values.yaml. It ensures consistency and easier updates across all services.

19. What’s your rollback strategy for failed Kubernetes deployments?

I use kubectl rollout undo deployment/<app> to revert to the previous stable version. In CI/CD, I automate this rollback if health checks fail post-deployment, ensuring quick recovery.

20. How do you ensure application-level logging in Kubernetes?

I use sidecar containers or ship logs via Fluentd/FluentBit to ELK Stack or CloudWatch Logs. This gives centralized visibility of app logs across all pods and namespaces.



Set 4 — AWS Core Services Deep-Dive

1. You uploaded files to S3 but they’re not accessible publicly. What do you check?

I first check the bucket policy and object ACLs — public access is blocked by default. Then I enable “Block Public Access: OFF” (if intentional), or configure CloudFront + OAI for secure public distribution.

2. How do you automate S3 backups for logs or reports?

I use S3 Lifecycle policies to move data to Glacier after X days and set Versioning + Cross-Region Replication for redundancy. For automation, I schedule Lambda triggered by CloudWatch Events to copy or archive files.

3. An IAM user reports “Access Denied” even with permissions. What’s your debugging approach?

I check for explicit Deny in policies, Service Control Policies (SCPs) from AWS Organizations, and whether permissions are on the correct resource ARN. Then, I simulate access via the IAM Policy Simulator to pinpoint the block.

4. How do you grant temporary access to an external consultant?

I create an IAM role with time-bound permissions and share it using STS (Security Token Service) via AssumeRole. This avoids creating permanent IAM users and ensures access auto-expires.

5. You can’t SSH into an EC2 instance. What do you check first?

I verify the key pair, security group (port 22), and network ACL. Then I check if the instance is in a private subnet or has no public IP. If locked out, I use EC2 Instance Connect or SSM Session Manager for access.

6. How do you securely manage SSH keys for EC2 in large teams?

I use AWS Systems Manager (Session Manager) to eliminate SSH keys. It logs sessions to CloudWatch and enforces IAM permissions — improving auditability and security.

7. You want to ensure that only specific IPs can access EC2. How?

I configure the Security Group inbound rule to allow only the desired IP/CIDR (e.g., office IP). I also verify NACL rules and use AWS WAF for extra protection if it’s a web server.

8. Your EC2 instance restarts randomly. What could be the reasons?

It might be due to underlying hardware failure, spot instance termination, or application crash. I check CloudWatch logs, EC2 system logs, and event history to identify root cause and set up Auto Recovery or ASG.

9. How do you create a private VPC with internet access only via NAT Gateway?

I create public and private subnets, attach IGW to the public subnet, and launch a NAT Gateway there. Then I route private subnet traffic to the NAT Gateway in route tables — ensuring secure outbound-only access.

10. You’re facing latency between EC2 instances in different AZs. How do you fix it?

I ensure both instances are in the same VPC and region. If cross-AZ traffic is required, I use placement groups (cluster type) or ENI for high-speed connections. Also check security groups and VPC Peering latency.

11. You deployed an RDS instance but the app can’t connect. What’s your approach?

I check RDS security group, subnet group, and endpoint hostname. Often, RDS is in a private subnet with no inbound access. I whitelist the EC2’s SG or use a bastion host for DB access.

12. How do you enable high availability for RDS?

I enable Multi-AZ deployment, which creates a standby replica in another AZ for failover. For scalability, I add Read Replicas to offload read-heavy queries. Both help improve uptime and performance.

13. You’re asked to automate database creation and network setup. What tool do you use?

I use AWS CloudFormation or Terraform for Infrastructure as Code. It defines RDS, VPC, and subnets declaratively — allowing version control and easy re-deployment.

14. How do you monitor CPU usage of EC2 and RDS instances?

I use CloudWatch metrics like CPUUtilization, DiskReadOps, and FreeStorageSpace. Then I set alarms to trigger SNS notifications when thresholds are breached — enabling proactive scaling or troubleshooting.

15. How do you automatically restart a failed EC2 instance?

Enable EC2 Auto Recovery under instance settings. It recreates the same instance in case of hardware failure — retaining EBS volumes, IPs, and metadata.

16. You need to balance traffic between multiple web servers. What’s your approach?

I configure an Application Load Balancer (ALB), register EC2s as targets, and enable health checks. For HTTPS, I attach an SSL certificate (ACM) and use sticky sessions if session persistence is required.

17. How do you redirect HTTP traffic to HTTPS on ALB?

In ALB listener rules, I add a rule on port 80 → redirect to port 443. This ensures all users are automatically routed through secure HTTPS connections.

18. How do you identify which EC2 instances are underutilized?

I use AWS Trusted Advisor or Compute Optimizer for recommendations. Then check CloudWatch CPU & network metrics. If usage is consistently low, I downsize the instance or move it to a smaller type.

19. How do you manage configurations across multiple environments (dev, test, prod)?

I maintain CloudFormation/Terraform templates with environment-specific variable files. I also use Parameter Store or Secrets Manager for environment-based secrets — ensuring consistency and isolation.

20. Your CloudFormation stack creation fails. How do you debug?

I check stack events in the AWS console — it shows which resource failed and why (e.g., permission denied or dependency missing). I fix the issue and rerun with stack rollback disabled for faster debugging.



Set 5 — CI/CD, Jenkins, GitHub Actions & Automation Pipelines

1. Your Jenkins pipeline failed after a code merge. What’s your debugging approach?

I first check the console output for the exact stage of failure — usually during build or test. Then I validate if the Git branch was merged properly, dependencies are up-to-date, and environment variables are correct. If it’s a new plugin or node issue, I restart Jenkins and test with a fresh workspace.

2. How do you securely store and use secrets in Jenkins pipelines?

I store secrets in the Jenkins Credentials Manager and access them using withCredentials() in pipelines. For higher security, I integrate Jenkins with AWS Secrets Manager or Vault. This ensures passwords/API keys are never exposed in logs or scripts.

3. How do you trigger a Jenkins pipeline automatically on code push?

I configure a webhook from GitHub or GitLab to Jenkins — it triggers a pipeline on a push or PR event. Alternatively, in GitHub Actions, I use:

on:
push:
branches: [ main ]


This ensures every commit is validated automatically.

4. Your build works locally but fails in Jenkins. What could be the cause?

It’s often due to environment differences — missing tools, wrong JDK, or path variables. I replicate the Jenkins environment locally using a Docker image to match configurations and fix the dependency or version mismatch.

5. How do you speed up a slow Jenkins pipeline?

I parallelize independent stages (e.g., build & test), use pipeline caching (like Maven or Docker layers), and move heavy builds to Jenkins agents with more CPU/memory. Also, I prune old builds/artifacts and use incremental builds when possible.

6. Your deployment stage in Jenkins failed midway. How do you ensure rollback?

I use blue-green deployment or canary release strategies. If a deployment fails, the pipeline triggers a rollback script that redeploys the last stable version from S3 or ECR, ensuring minimal downtime.

7. How do you implement CI/CD for a Spring Boot app on AWS EC2?

I configure a pipeline where:

Jenkins builds the JAR using Maven.

Uploads it to S3.

SSHs into EC2 and deploys the app (via Ansible or shell script).
CloudWatch monitors the health and restarts the app if needed — a fully automated deployment loop.

8. How do you handle environment-specific variables in pipelines (dev/test/prod)?

I use parameterized Jenkins pipelines or .env files stored in S3/Parameter Store. In GitHub Actions, I define env per job or use separate YAMLs. This avoids hardcoding credentials and keeps environments isolated.

9. How do you handle a failed stage but still continue the pipeline?

In Jenkins declarative pipeline:

catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
sh 'run-tests.sh'
}


This logs the failure but lets the pipeline continue — useful for non-critical checks like linting or code coverage.

10. How do you deploy a Dockerized app using Jenkins?

The pipeline:

Builds Docker image → tags it → pushes to ECR/DockerHub.

SSHs into EC2 or triggers Kubernetes deployment via kubectl.
I use Jenkins credentials for Docker login and AWS CLI for authentication — ensuring full CI/CD automation.

11. How do you handle Jenkins master node becoming unavailable?

I maintain Jenkins configuration backup (via ThinBackup plugin or S3 cron sync). For HA, I use Jenkins controller + agents model, or host Jenkins on EKS with persistent volume — allowing auto-recovery and scaling.

12. How do you implement approvals before production deployment?

I use input() in Jenkins pipelines to pause execution until manual approval. In GitHub Actions, I use “environment protection rules” for approval before deploy jobs proceed to production.

13. Your Jenkins job suddenly stopped running. What could be wrong?

Possible causes:

Jenkins agent offline

Disk full

Credential expiration

SCM webhook broken.
I check /var/log/jenkins/jenkins.log, restart the service, and verify node connectivity + job queue status.

14. How do you prevent multiple Jenkins jobs from running simultaneously?

I use the “Throttle Concurrent Builds” or “Lockable Resources” plugin. It ensures that resource-heavy jobs or shared resources (like EC2 or DB) aren’t accessed by parallel builds.

15. How do you deploy an app automatically after every successful build?

After the build stage passes, I add a post { success { ... } } block in the pipeline to trigger deployment. Alternatively, I use GitHub Actions + AWS CodeDeploy to automate rollout post-successful build.

16. You want to run nightly jobs for health checks. How do you do that?

I schedule a CRON job in Jenkins (H 0 * * * → every midnight). The job runs scripts that verify API health, log size, or backup status, sending Slack/email alerts via plugins.

17. How do you store Jenkins build artifacts for later use?

I use the archiveArtifacts directive or push artifacts (like .jar or .zip) to S3 or Nexus repository. This allows rollback or redeployment anytime without rebuilding code.

18. How do you integrate testing in your CI/CD pipeline?

I add a dedicated test stage:

stage('Test') {
steps {
sh 'mvn test'
}
}


If tests fail, pipeline halts. For UI/API tests, I use Selenium or Postman collections integrated with Jenkins.

19. How do you handle credentials rotation without pipeline failures?

I use AWS Secrets Manager or Jenkins Credentials Binding Plugin. When secrets rotate, I update them centrally — pipelines automatically pick new values without code changes.

20. How do you debug a GitHub Actions workflow that fails?

I enable debug logging using ACTIONS_STEP_DEBUG=true, re-run the workflow, and inspect logs. Often, it’s due to missing permissions or incorrect YAML syntax. I test locally using act CLI before pushing changes.


Set 6 — Docker, Kubernetes & Containerization

1. Your Docker container fails immediately after starting. How do you troubleshoot?

I check the container logs using docker logs <container_id>. Often it’s due to missing environment variables, incorrect CMD/ENTRYPOINT, or missing dependencies. I replicate locally, fix Dockerfile, and rebuild.

2. How do you optimize Docker image size?

I use multi-stage builds to keep only essential artifacts, choose slim/base images, and remove unnecessary packages. This reduces build time, speeds up deployment, and lowers storage cost.

3. Your application works locally but crashes on Kubernetes. How do you debug?

I check kubectl get pods for pod status, then kubectl describe pod <pod> to see events. Logs via kubectl logs <pod> help identify container errors. Resource limits or missing ConfigMaps/Secrets often cause crashes.

4. How do you handle persistent storage in Kubernetes?

I use PersistentVolume (PV) and PersistentVolumeClaim (PVC) to attach storage to pods. For example, storing DB data on EBS volumes ensures data survives pod restarts or redeployments.

5. Your pod is in CrashLoopBackOff. What’s your approach?

Check kubectl logs for errors. Verify environment variables, mounted volumes, container image, and resource limits. If init containers fail, I debug them separately. Fixing configuration usually resolves it.

6. How do you scale Kubernetes deployments?

I use kubectl scale deployment <name> --replicas=N or configure Horizontal Pod Autoscaler (HPA) for dynamic scaling based on CPU/memory metrics. For high traffic, HPA automatically adds pods.

7. How do you update a running Kubernetes deployment without downtime?

I use Rolling Updates via kubectl apply -f deployment.yaml. Kubernetes gradually replaces old pods with new ones. If something breaks, I use kubectl rollout undo deployment/<name> to rollback.

8. How do you manage configuration for multiple environments in Kubernetes?

I use ConfigMaps for app configuration and Secrets for sensitive info. Different YAML files or Helm values are applied per environment (dev, staging, prod) without changing the image.

9. Your pod can’t reach an external service. What could be wrong?

Likely causes: wrong DNS, missing network policies, or misconfigured service endpoints. I use kubectl exec -it <pod> -- ping <service> and check kubectl get svc and kubectl get networkpolicies.

10. How do you handle Docker image versioning in CI/CD?

I use semantic versioning and tag images with commit SHA or build number. Jenkins/GitHub Actions pushes images to ECR/DockerHub, ensuring traceability and safe rollbacks.

11. How do you reduce cold start time for containers?

Use lightweight base images, pre-pulled images on nodes, and keep container initialization scripts minimal. For serverless containers, warm-up hooks reduce startup latency.

12. How do you monitor Kubernetes clusters?

I deploy Prometheus + Grafana to collect metrics, configure alerting rules, and track pod, node, and service health. Logs are shipped to ELK stack for debugging production issues.

13. How do you perform zero-downtime deployment for stateful apps?

I use StatefulSets with PVs, update replicas one at a time, and maintain read/write replicas. Careful volume handling ensures data is consistent during rolling upgrades.

14. How do you debug networking issues between pods?

I use kubectl exec to test connectivity (ping, curl) between pods. Check services, endpoints, DNS, and network policies. Tools like kubectl port-forward and nslookup help trace routing issues.

15. How do you clean unused Docker images and containers?

I run docker system prune -a to remove stopped containers, dangling images, and unused networks. This frees space and avoids conflicts during new builds.

16. Your pod’s CPU is high, affecting performance. How do you fix it?

I set resource requests and limits in deployment YAML. HPA can automatically scale pods. For heavy workloads, I optimize code or split services into microservices for load distribution.

17. How do you handle secrets in Kubernetes?

Use Kubernetes Secrets or integrate Vault/Secrets Manager. Avoid storing sensitive info in ConfigMaps or container images. I mount secrets as environment variables or files inside pods.

18. How do you roll back a failed Kubernetes deployment?

Use kubectl rollout undo deployment/<name>. Kubernetes restores the last known working replica set, ensuring the system returns to stable state without manual redeployment.

19. How do you integrate Docker & Kubernetes with Jenkins?

Pipeline steps:

Build Docker image → tag → push to ECR/DockerHub.

Apply Kubernetes manifests using kubectl or Helm.

Trigger pipeline post-successful code push.
Credentials stored securely in Jenkins for Docker login and cluster access.

20. How do you debug container startup issues caused by missing libraries?

Check docker logs or kubectl logs. If libraries are missing, update Dockerfile with apt-get install or package manager commands. Rebuild the image and redeploy.



Set 7 — AWS Services (EC2, S3, VPC, IAM, Networking, Load Balancer)

1. Your EC2 instance is not reachable via SSH. How do you troubleshoot?

Check security groups (port 22 open), network ACLs, and instance public IP. Verify key pair matches the instance. Use ping or telnet to test connectivity. For persistent issues, check instance system logs in the AWS console.

2. Your EC2 instance CPU is high. How do you handle it?

Check running processes (top, htop). Identify resource-heavy apps. Consider upgrading instance type, adding Auto Scaling, or offloading tasks to separate instances. Use CloudWatch alarms to monitor CPU utilization.

3. S3 bucket access is denied for your app. What do you check?

Verify bucket policy, IAM role/policy, and object ACLs. Ensure the app uses proper access keys or instance role. Test using AWS CLI: aws s3 ls s3://bucket-name.

4. How do you make S3-hosted website highly available?

Enable static website hosting, configure bucket policy for public read, enable CloudFront with S3 origin for caching, HTTPS, and global distribution. Enable versioning for rollback and durability.

5. Your EC2 instances are in a private subnet and need internet. How do you enable this?

Deploy a NAT Gateway in a public subnet and update route tables of the private subnet. EC2 routes internet traffic through NAT to access updates, patches, or APIs securely.

6. You need to automate infrastructure creation in AWS. How do you do it?

Use Terraform or CloudFormation. Define EC2, VPC, subnets, security groups, and IAM roles as code. This ensures reproducibility, version control, and faster provisioning.

7. Your ELB health checks are failing. How do you debug?

Check security groups (allow LB to reach instances). Ensure instance app is listening on correct port and path. Use curl internally to confirm response. Update health check path or thresholds if needed.

8. How do you secure your EC2 instances?

Use security groups, IAM roles, and OS-level firewall. Disable root login, use SSH keys, patch OS regularly, and enable CloudTrail for auditing. Avoid storing secrets on instances directly.

9. How do you handle cross-region disaster recovery for EC2 & S3?

Create AMI backups and replicate S3 buckets across regions. Use Route53 with health checks to failover traffic. Automate backups using Lambda or Lifecycle policies.

10. Your EC2 instance is stuck at pending state. What do you check?

Check subnet capacity and AZ resource limits. Verify instance type availability. Check security groups, key pair, and IAM permissions. Sometimes AWS quota limits cause pending states.

11. How do you rotate IAM access keys?

Enable IAM best practices. Generate new key, update apps/CLI, verify functionality, then deactivate old key. Avoid hardcoding keys; prefer IAM roles for EC2/Lambda.

12. How do you monitor AWS resources?

Use CloudWatch metrics, dashboards, and alarms. Track EC2 CPU, memory (via CloudWatch agent), ELB request count, S3 bucket size, and API errors. Set automated notifications using SNS.

13. How do you implement cost optimization for EC2?

Use Spot Instances for non-critical workloads, Reserved Instances for long-term usage. Enable Auto Scaling, right-size instances using CloudWatch metrics, and shutdown idle instances automatically.

14. Your Lambda function can’t access S3. How do you fix it?

Attach proper IAM role to Lambda with s3:GetObject or required permissions. Verify bucket policy allows Lambda execution. Check VPC/subnet/NAT if Lambda runs in private VPC.

15. How do you secure S3 data?

Enable Server-Side Encryption (SSE-S3/SSE-KMS), restrict bucket policies, disable public access, enable MFA delete. Use CloudTrail to monitor access events.

16. Your EC2 instance can’t reach another instance in same VPC. How do you debug?

Check security groups (allow inbound/outbound), network ACLs, instance subnet, and routing table. Ping using private IP to confirm connectivity. Use traceroute for network path check.

17. How do you automate EC2 deployment in CI/CD?

Use Terraform/CloudFormation to provision instances. Integrate with Jenkins pipeline: build → test → deploy → update security groups and AMIs. Use Ansible for post-deployment configuration.

18. How do you handle logging in AWS?

Use CloudWatch Logs for EC2, Lambda, and applications. Stream logs from S3 or instances. Aggregate with ELK/CloudWatch Insights for monitoring and debugging.

19. How do you manage VPC subnets for public & private resources?

Create public subnet for NAT/ELB and private subnet for EC2. Use route tables to control traffic. Deploy DB in private subnet for security. Attach NAT for private instances to access internet.

20. Your EC2 instance lost connectivity after reboot. What could be wrong?

Check Elastic IP (if not attached, public IP changes), security groups, and VPC route tables. Verify instance network configuration. Reattach Elastic IP if needed for static connectivity.


Set 8 — CI/CD & Jenkins Scenarios

1. Your Jenkins pipeline fails during build. How do you troubleshoot?

Check Jenkins console logs for errors. Verify build environment, dependencies, and Maven/Gradle configurations. Ensure proper Java version, check workspace cleanup, and validate Git repo access.

2. How do you trigger Jenkins pipeline automatically on code push?

Configure webhooks in GitHub/GitLab to notify Jenkins. Use Multibranch Pipeline or Pipeline Job with SCM Polling or GitHub hook trigger. Test by pushing a commit to see pipeline execution.

3. How do you manage secrets in Jenkins pipelines?

Use Jenkins Credentials Plugin to store secrets, passwords, and API keys. Access them in pipeline using credentials() or environment variables. Avoid hardcoding secrets in scripts.

4. Jenkins slave node is offline. How do you fix it?

Check agent logs for errors. Ensure Java version matches master requirements. Verify network connectivity, proper SSH key or JNLP config, and that agent service is running.

5. How do you handle multiple environments (dev/stage/prod) in CI/CD?

Use parameterized builds or Jenkinsfile with environment variables. Maintain separate credentials and config files per environment. Deploy to each environment using conditional stages.

6. How do you rollback a failed deployment in Jenkins?

Maintain artifact versioning (e.g., via Maven or Nexus). On failure, trigger rollback stage to redeploy last stable artifact. Automate rollback in pipeline script for quick recovery.

7. Your Jenkins job times out during build. What could be wrong?

Check build server resources (CPU, memory). Validate network connectivity for dependencies. Increase timeout configuration in pipeline or split tasks into smaller stages.

8. How do you deploy Dockerized apps using Jenkins?

Install Docker plugin. In pipeline:

Build image (docker build).

Push to Docker registry (Docker Hub/ECR).

Deploy to target (EC2/Kubernetes). Use credentials plugin for registry authentication.

9. How do you handle pipeline failures in multi-stage deployment?

Implement try/catch or post blocks in Jenkinsfile. Send notifications on failure via email or Slack plugin. Use atomic stages to prevent partial deployment.

10. How do you integrate Jenkins with GitHub Actions?

Use webhooks or GitHub plugin in Jenkins. Trigger pipeline on PR/commit. Optionally, Jenkins can call GitHub Actions via REST API for specialized workflows.

11. How do you version artifacts for CI/CD?

Use Maven/Gradle to create versioned JARs/WARs. Store in Nexus/Artifactory. Include build number or commit hash in version. Jenkins can automatically increment build number.

12. How do you test pipeline changes safely?

Use sandbox/testing branch in GitHub. Configure Jenkins to run on that branch. Validate build, deploy, and rollback scripts before merging into main pipeline.

13. How do you implement canary deployment in Jenkins?

Deploy new version to a subset of servers first. Monitor metrics/logs. Gradually shift traffic using load balancer or Kubernetes deployment strategies. Automate using Jenkins stages.

14. Jenkins build fails due to missing dependency. How do you fix it?

Check dependency repository (Nexus/Maven Central). Ensure correct version in pom.xml/build.gradle. Update proxy settings if network blocks dependency download.

15. How do you deploy to multiple regions using CI/CD?

Use parameterized pipeline stages with region as variable. Deploy same artifact to different AWS regions. Include region-specific configs or environment variables.

16. How do you monitor Jenkins job execution?

Use built-in console output, Blue Ocean plugin, and email/Slack notifications. Integrate Prometheus/Grafana with Jenkins exporter for metrics like build duration, success rate.

17. How do you handle large artifacts in Jenkins?

Use artifact repository (Nexus/Artifactory). Avoid storing directly in Jenkins workspace. Enable artifact retention policy to delete old builds.

18. Jenkins pipeline fails intermittently at test stage. How do you debug?

Check test logs for environment-specific issues. Re-run in isolated environment. Validate dependencies, DB connection, network, or timeouts. Consider reliable test data.

19. How do you automate database migrations in CI/CD?

Use Flyway/Liquibase integrated in pipeline. Run migration scripts before deployment. Include rollback scripts in case migration fails.

20. How do you secure Jenkins server?

Enable authentication (LDAP/GitHub). Use credentials plugin for secrets. Restrict job permissions, disable anonymous access, enable HTTPS, and regularly update plugins.



Set 9 — Docker & Kubernetes Scenarios

1. Your Docker container fails to start. How do you debug it?

Check container logs using docker logs <container>. Verify Dockerfile configuration, environment variables, and mounted volumes. Use docker run -it <image> for interactive testing.

2. How do you build and push a Docker image to AWS ECR?

Authenticate with aws ecr get-login-password.

Build image with docker build -t <repo>:<tag>.

Tag image with ECR URI.

Push using docker push <ECR_URI>.

3. Kubernetes pod is in CrashLoopBackOff. How do you troubleshoot?

Check kubectl describe pod <pod> for events and kubectl logs <pod> for application errors. Ensure image exists, env variables, resource limits, and config maps/secrets are correct.

4. How do you scale a deployment in Kubernetes?

Use kubectl scale deployment <name> --replicas=<count>. For auto-scaling, configure Horizontal Pod Autoscaler using CPU/memory metrics.

5. How do you handle rolling updates in Kubernetes?

Use kubectl apply -f deployment.yaml. Kubernetes performs rolling updates by updating pods gradually. Monitor with kubectl rollout status deployment <name>.

6. How do you rollback a failed Kubernetes deployment?

Use kubectl rollout undo deployment <name> to revert to the previous working version. Always keep versioned Docker images to ensure rollback works.

7. How do you manage secrets in Kubernetes?

Use kubectl create secret (generic or docker-registry). Mount secrets as environment variables or volumes. Encrypt sensitive data at rest with KMS or Sealed Secrets.

8. How do you debug networking issues between pods?

Check service, endpoints, and pod IPs using kubectl get svc and kubectl get pods -o wide. Use kubectl exec <pod> -- ping <pod> to test connectivity. Verify Network Policies.

9. How do you monitor a Kubernetes cluster?

Use Prometheus + Grafana for metrics. Check kube-state-metrics and node/pod health. Enable alerts for CPU, memory, and pod failures.

10. How do you run a multi-container app in Kubernetes?

Define Deployment/Pod with multiple containers. Use Init containers if needed. Communicate via localhost or shared volumes. Ensure proper readiness/liveness probes.

11. How do you clean up unused Docker images and containers?

Use docker system prune -a to remove stopped containers, dangling images, and unused networks. Helps free disk space on servers.

12. How do you configure persistent storage for Kubernetes pods?

Use PersistentVolume (PV) + PersistentVolumeClaim (PVC). Mount PV in pods for data persistence. Use StorageClass for dynamic provisioning.

13. How do you handle resource limits in Kubernetes?

Define requests and limits in pod specs. Prevent CPU/memory exhaustion and OOMKilled errors. Use Horizontal/Vertical autoscaler to handle scaling.

14. How do you deploy an app on AWS EKS?

Configure kubectl with EKS cluster.

Apply Deployment/Service manifests.

Expose using LoadBalancer service.

Use Helm for complex apps.

15. How do you implement blue-green deployment in Kubernetes?

Deploy new version to a separate namespace or deployment. Switch traffic using Ingress or service selector. Rollback is simple by reverting the service.

16. Kubernetes pod is not getting an IP. What do you check?

Check CNI plugin status (Calico, Flannel). Validate node network config. Verify kubelet logs and kubectl describe pod.

17. How do you update environment variables in running pods?

Update ConfigMap/Secret, then restart pods using kubectl rollout restart deployment <name> for changes to take effect.

18. How do you implement CI/CD for Kubernetes deployments?

Use Jenkins/GitHub Actions:

Build Docker image

Push to registry

Apply manifests to cluster

Monitor rollout status

19. How do you debug image pull errors in Kubernetes?

Check kubectl describe pod <pod> for imagePullBackOff reason. Verify image exists, correct registry credentials, and network access.

20. How do you expose a Kubernetes app externally?

Use Service type LoadBalancer for cloud provider. Alternatively, use Ingress Controller for routing. Apply TLS/HTTPS using cert-manager if needed.



Set 10 — Terraform & Infrastructure as Code (IaC) Scenarios

1. How do you provision an EC2 instance using Terraform?

Define a resource "aws_instance" in a .tf file with AMI, instance type, key pair, and security group. Run terraform init, terraform plan, then terraform apply to provision. Useful for repeatable infrastructure.

2. How do you manage sensitive variables in Terraform?

Use variable blocks with sensitive = true, or store secrets in AWS Secrets Manager / SSM Parameter Store and reference via Terraform. Prevents exposing secrets in logs.

3. Terraform plan shows a drift in infrastructure. How do you fix it?

Run terraform plan to see differences. Apply with terraform apply to sync. For manual changes outside Terraform, consider importing resources with terraform import.

4. How do you organize Terraform code for multiple environments?

Use workspaces, modules, or separate directories (dev, staging, prod). Avoid hardcoding values; use variables.tf and terraform.tfvars per environment.

5. Terraform apply fails due to IAM permissions. How do you troubleshoot?

Check user/role policies in AWS. Ensure Terraform’s execution role has ec2:Create*, s3:*, or necessary permissions. Use debug logs (TF_LOG=DEBUG) for details.

6. How do you use Terraform modules?

Modules are reusable blocks of Terraform code. Define inputs/outputs, call via module "name" { source = "./module_path" }. Helps maintain DRY and scalable infra.

7. How do you handle dependencies between resources?

Terraform manages dependencies automatically using references (${aws_vpc.main.id}). Use depends_on only when explicit ordering is needed. Prevents race conditions in provisioning.

8. How do you destroy all resources safely?

Use terraform destroy. Check plan first to avoid accidental deletion. For production, consider targeted destroy using -target to remove only specific resources.

9. How do you manage Terraform state files securely?

Use remote backends like S3 + DynamoDB for locking. Prevents state conflicts in team environments. Encrypt state files using KMS.

10. How do you handle Terraform errors like “Resource already exists”?

Use terraform import to bring existing resources under management. Avoid manual deletion unless necessary. Ensures IaC and real infra stay in sync.

11. How do you update an existing EC2 instance configuration?

Modify .tf file (instance type, security groups). Run terraform plan → review changes → terraform apply. Changes are applied without recreating unrelated resources.

12. How do you provision RDS using Terraform?

Use resource "aws_db_instance" with engine, instance class, storage, username/password (via secrets). Ensure backup, multi-AZ, and security groups are configured for production.

13. Terraform state got corrupted. How do you recover?

Restore from S3 remote backend versioning, or use terraform state pull to retrieve last known good state. Rebuild manually only as last resort.

14. How do you create a VPC with subnets using Terraform?

Use aws_vpc + aws_subnet resources. Tag subnets as public/private. Associate route tables, IGW, NAT. Modularize for reusability across projects.

15. How do you use variables in Terraform?

Define in variables.tf, provide defaults or override via terraform.tfvars. Example: variable "instance_type" { default = "t2.micro" }. Avoid hardcoding for flexibility.

16. How do you provision Lambda using Terraform?

Use aws_lambda_function with S3 bucket or ZIP file, role ARN, runtime, handler. Combine with API Gateway for REST endpoints. Automates serverless deployment.

17. How do you integrate Terraform with CI/CD?

Use Jenkins/GitHub Actions:

terraform fmt → terraform init → terraform plan → terraform apply

Use workspaces per environment and remote state to ensure team safety.

18. How do you handle provider version conflicts?

Specify provider version in required_providers block. Run terraform init -upgrade to update. Prevents breaking changes across modules or projects.

19. How do you monitor Terraform deployments?

Use plan output and Terraform Cloud/Enterprise dashboards. Track resource changes, drift detection, and audit logs for production environments.

20. How do you automate infrastructure rollback?

Store previous Terraform state in remote backend. Run terraform apply with older state reference or revert specific resources using -target. Enables fast recovery after errors.


Set 11 — Monitoring, Logging & DevSecOps Scenarios

1. How do you set up monitoring for a Kubernetes cluster?

Use Prometheus + Grafana: deploy Prometheus to scrape metrics from pods/nodes, configure alert rules, and visualize with Grafana dashboards. Helps detect CPU/memory spikes, pod restarts, or failing deployments.

2. How do you troubleshoot alerts in Prometheus?

Check alert rules and thresholds, query metrics in Prometheus UI, and inspect affected pods/nodes. For example, high CPU alert → verify pods, check HPA, and scaling config. Document root cause for future reference.

3. How do you log application errors in production?

Use ELK Stack: Filebeat ships logs to Logstash → Elasticsearch → visualize in Kibana. Allows searching, filtering, and alerting for errors or anomalies in logs.

4. How do you monitor cloud infrastructure costs?

Use AWS Cost Explorer or Azure Cost Management, set budgets and alerts, and tag resources for accountability. Helps identify over-provisioned instances or unused services.

5. How do you secure secrets in CI/CD pipelines?

Store secrets in Vault, AWS Secrets Manager, or Azure Key Vault, inject at runtime using environment variables. Avoid storing credentials in Git or pipeline scripts.

6. How do you implement role-based access in Kubernetes?

Use RBAC: define Role or ClusterRole and bind with RoleBinding/ClusterRoleBinding. Limits access to namespaces or cluster-wide resources, enhancing security and compliance.

7. How do you handle a breached API key?

Immediately revoke the key, update all environments, rotate credentials, and review audit logs to track unauthorized access. Automate key rotation in future deployments.

8. How do you enforce pipeline security?

Integrate SAST/DAST tools, run linting, vulnerability scans, enforce branch protection, and require code reviews. Prevents malicious code or insecure dependencies from reaching production.

9. How do you monitor microservices performance?

Use distributed tracing (Jaeger/Zipkin) + metrics (Prometheus). Track request latency, error rates, and throughput per service. Helps quickly locate slow or failing services.

10. How do you debug slow application response in production?

Check logs, metrics, and traces: CPU/memory usage, DB queries, network latency. Identify bottlenecks → scale pods, optimize queries, or tune cache. Document steps for reproducibility.

11. How do you secure SSH access to servers?

Disable root login, use key-based authentication, restrict access via security groups/firewalls, and enforce 2FA if supported. Regularly rotate keys.

12. How do you implement alerting for failed deployments?

Integrate CI/CD pipeline with Slack/email alerts. Use Prometheus alert rules to monitor deployment status, container health, and notify the team for immediate action.

13. How do you handle secrets in Kubernetes?

Use Kubernetes Secrets, mount as environment variables or files, encrypt at rest (via KMS), and restrict access with RBAC. Avoid hardcoding secrets in manifests.

14. How do you monitor server disk usage?

Deploy Node Exporter for Prometheus, monitor / and /var/log, set alerts at thresholds (e.g., 80%). Helps prevent outages due to full disks.

15. How do you perform a security audit on AWS resources?

Use AWS Security Hub, IAM Access Analyzer, Config rules, and review open security groups, unused keys, and S3 bucket policies. Mitigate risks with automated remediation.

16. How do you detect and respond to production incidents?

Set up centralized logging, monitoring, and alerting. Investigate metrics/logs → isolate issue → rollback or patch. Conduct postmortems to prevent recurrence.

17. How do you rotate database credentials securely?

Use AWS Secrets Manager or HashiCorp Vault to automate rotation. Update dependent services via environment variables or config maps to avoid downtime.

18. How do you prevent sensitive info leaks in logs?

Mask passwords/API keys, configure log filters, and avoid logging sensitive request payloads. Use structured logging for better search and auditing.

19. How do you secure container images?

Scan with Trivy or Clair, enforce signed images, minimize base image vulnerabilities, and use immutable tags. Ensures only trusted images run in production.

20. How do you implement proactive monitoring for high availability?

Set SLIs/SLOs/SLAs, monitor latency, error rates, traffic, and set auto-scaling rules. Alerts should trigger before SLA breach, enabling quick remediation.


Set 12 — CI/CD & Automation Scenarios

1. How do you set up a Jenkins pipeline for a Java Spring Boot app?

Create a Jenkinsfile with stages: checkout → build → test → package → deploy. Use Maven or Gradle for builds and Docker to containerize. Automate deployment to EC2 or Kubernetes for faster iterations.

2. How do you handle pipeline failures?

Check Jenkins logs, identify failing stages, inspect console output. Common issues: dependency errors, test failures, or permission issues. Fix root cause and rerun pipeline. Implement notifications for quick alerts.

3. How do you implement automated testing in CI/CD?

Integrate unit tests, integration tests, and static code analysis into pipeline stages. Fail pipeline if tests fail. For example, use JUnit for Java, pytest for Python, or SonarQube for code quality.

4. How do you deploy a containerized app using GitHub Actions?

Define a workflow YAML with jobs: checkout → build Docker image → push to Docker Hub/ECR → deploy to Kubernetes/EC2. Automate triggers on pull requests or merges to main branch.

5. How do you rollback a failed deployment?

Use immutable deployments with Docker/Kubernetes. If a new deployment fails, rollback to previous stable version using kubectl rollout undo or by redeploying previous image. Maintain versioned artifacts in repository.

6. How do you implement secrets in CI/CD pipelines?

Use Jenkins credentials plugin, GitHub Secrets, or Vault. Inject secrets as environment variables at runtime. Avoid hardcoding sensitive information in scripts.

7. How do you automate infrastructure provisioning?

Use Terraform or CloudFormation: define resources as code, plan → apply → destroy. Example: provision EC2 + S3 + RDS for a Spring Boot app, ensuring repeatable environments.

8. How do you handle concurrent deployments in CI/CD?

Use locking or queuing mechanisms in Jenkins (lock step) or GitHub Actions (concurrency key) to avoid race conditions. Ensures multiple deployments don’t overwrite each other.

9. How do you manage pipeline artifacts?

Store build artifacts in Artifactory, Nexus, or S3, version them, and use in downstream stages. Example: package .jar file in Maven → push to artifact repo → deploy to EC2/K8s.

10. How do you implement pipeline notifications?

Integrate with Slack, Teams, or email using plugins or webhooks. Notify success, failure, or deployment status. Example: Jenkins Slack plugin sends alerts if build fails at test stage.

11. How do you test infrastructure changes before production?

Use staging or dev environments, run Terraform plan/dry-run, and automate tests for configuration changes. Catch errors before impacting production.

12. How do you handle secrets rotation in CI/CD?

Rotate API keys or passwords in Vault or AWS Secrets Manager, update pipeline variables, and restart jobs if necessary. Automate rotation to minimize manual errors.

13. How do you implement blue-green deployments?

Maintain two environments (blue & green). Deploy new version to green → test → switch traffic via load balancer. Ensures zero downtime and easy rollback.

14. How do you integrate security scanning in pipelines?

Add SAST/DAST tools in CI stage. Example: Jenkins stage runs SonarQube or Trivy scan → fail build if vulnerabilities detected. Promotes DevSecOps culture.

15. How do you deploy multi-service applications in CI/CD?

Use multi-stage pipelines: each service has build/test/deploy stage. Use Docker Compose or Kubernetes manifests to coordinate deployments. Maintain versioned images for rollback.

16. How do you debug pipeline timeout issues?

Check agent logs, network connectivity, and resource limits. For Jenkins, verify executor availability. Adjust timeout parameters or optimize build steps.

17. How do you implement canary deployments?

Deploy new version to small subset of users → monitor metrics → gradually increase traffic if stable. Use Kubernetes services or load balancer rules for routing.

18. How do you automate rollback in CI/CD?

Add post-failure hooks: if deployment fails, trigger rollback job to previous stable artifact. Example: Jenkins post { failure { ... } } block or GitHub Actions if: failure().

19. How do you monitor CI/CD pipeline health?

Track pipeline duration, success/failure rate, agent status, and queue length. Use Jenkins Dashboard, GitHub Actions Insights, or Grafana. Helps detect bottlenecks early.

20. How do you version control infrastructure?

Keep Terraform, Ansible, Helm charts in Git repos. Use branches for feature/dev/test. Review changes via PRs before merging to main. Ensures auditability and reproducibility.


