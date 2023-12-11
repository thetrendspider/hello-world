# ECS Task Restart Runbook

## Overview
This runbook provides step-by-step instructions to restart a task in Amazon ECS.

## Prerequisites
1. AWS CLI installed and configured with appropriate IAM permissions.
2. ECS task definition and cluster already set up.

## Procedure

### 1. Identify the ECS Cluster and Task to Restart
   - Log in to the AWS Management Console.
   - Navigate to the ECS service.
   - Identify the ECS cluster and task that you want to restart.

### 2. Stop the Running Task
   - Open a terminal or command prompt.
   - Execute the following AWS CLI command to stop the running task:
     ```bash
     aws ecs stop-task --cluster YOUR_CLUSTER_NAME --task YOUR_TASK_ID
     ```

### 3. Verify the Task Stopped
   - Check the ECS console or use the following AWS CLI command to verify that the task has stopped:
     ```bash
     aws ecs describe-tasks --cluster YOUR_CLUSTER_NAME --tasks YOUR_TASK_ID
     ```
   - Ensure that the task state is `STOPPED`.

### 4. Start a New Task
   - Execute the following AWS CLI command to start a new task using the same task definition:
     ```bash
     aws ecs run-task --cluster YOUR_CLUSTER_NAME --task-definition YOUR_TASK_DEFINITION
     ```

### 5. Monitor the New Task
   - Monitor the ECS console or use the following AWS CLI command to check the status of the new task:
     ```bash
     aws ecs describe-tasks --cluster YOUR_CLUSTER_NAME --tasks NEW_TASK_ID
     ```

### 6. Verify the Restart
   - Confirm that the new task is running successfully, and the application is operational.

## Additional Notes
- Ensure that the ECS task definition and associated resources are properly configured.
- Review ECS and ECS Task documentation for more advanced configurations.


