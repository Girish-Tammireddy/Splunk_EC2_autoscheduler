# Splunk_EC2_autoschedule
EC2 _autoscheduling 

#Ec2 automated turn-on / off functionality for DR purposes:

Solution:
We are using the following AWS resources to accomplish the above functionality

a.IAM role for Lambda execution:
This IAM role will be assumed by the Lambda function to execute the necessary start / stop Ec2 functionality and to write the logs to cloud watch logs.

b.Evenbridge:
We will be using the AWS event bridge rules to create a pattern which would match the event pattern of an EC2 instance state changing to stopping , shutting down or starting , based on these events the rule will be invoking the corresponding Lambda functions .

c.Lambda:
There will be 2 lambda functions used in this framework one for starting  the ec2 instance - this gets triggered when the primary EC2 instance goes into stopping , shutting down or terminating state from running state .

A second lambda function will be used to stop the secondary Ec2 in DR when the primary Ec2 instance changes it state to running .



# Solution Deployment:
To Deploy the solution , get started by deploying the IAM_Role_lambda.yaml CFN template first and save the ARN of the IAM role created which we will be using later as input parameter for the other templates

Next insert the instance id of the secondary ec2 in the Lambda function in the place holder field  " instances = ['i-081fc9a044eaa945d'] " and deploy the Lambda-ec2-TurnOFF.yaml and theLambda-ec2-TurnON.yaml templates pass the ARN of the IAM role created in the previous step as input parameters

In the third step deploy the sns-eventrule-ec2turnoff.yaml sns-eventrule-ec2turnofN.yaml CFN template.

