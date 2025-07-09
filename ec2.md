1. Showing all ec2 instances

``
aws ec2 describe-instances --query 'Reservations[].Instances[].{ID:InstanceId,IP:PublicIpAddress,Name:Tags[?Key==`Name`]|[0].Value}' --output table`
``

2. Terminate EC2 Instance

``
aws ec2 terminate-instances --instance-ids instance-name
``