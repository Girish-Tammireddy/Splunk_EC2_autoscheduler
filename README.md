# Splunk_EC2_autoschedule
EC2 _autoscheduling 

Ec2 automated turn-on / off functionality for DR purposes:

We are using the following AWS resources to accomplish the above functionality

a.IAM role for Lambda execution:
This IAM role will be assumed by the Lambda function to execute the necessary start / stop Ec2 functionality and to write the logs to cloud watch logs.

b.Evenbridge:
We will be using the AWS event bridge rules to create a pattern which would match the event pattern of an EC2 instance state changing to stopping , shutting down or starting , based on these events the rule will be invoking the corresponding Lambda functions .

c.Lambda:
There will be 2 lambda functions used in this framework one for starting  the ec2 instance - this gets triggered when the primary EC2 instance goes into stopping , shutting down or terminating state from running state .

A second lambda function will be used to stop the secondary Ec2 in DR when the primary Ec2 instance changes it state to running .

A VPC endpoint connection across the regions would be needed for the lambda to access the Ec2 in secondary VPC from primary region.


To Deploy the solution , get started by deploying the 

aws cloudformation deploy --template-file /path_to_template/template.json --stack-name my-new-stack --parameter-overrides Key1=Value1 Key2=Value2 --tags Key1=Value1 Key2=Value2
