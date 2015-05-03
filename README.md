# seattleaws
Seattle AWS Architects &amp; Engineers


## Command Line Stack Setup
### Setup your AWS keys

Create an [access key](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSGettingStartedGuide/AWSCredentials.html) if you haven't done so already

I use the following shell script and it is necessary to source the script (notice the extra ". " at the beginning)
```
. ~/.ssh/aws_keys.sh
```
The shell script is
```bash
#!/bin/bash
export AWS_ACCESS_KEY_ID=<Your Access key>
export AWS_SECRET_ACCESS_KEY=<Your secret key>
```

### Kick off the stack creation (or cloud formation)

Run the following command line
```
aws cloudformation create-stack --stack-name <stack name> --template-body file://awsmeetup.json --parameters ParameterKey=ParamKeyName,ParameterValue=<Your key filename> ParameterKey=ParamSshCidr,ParameterValue=<your IP address - use https://www.whatismyip.com/>
```
My specific command line is:
```
aws cloudformation create-stack --stack-name seattle-aws-soln-arch-05 --template-body file://awsmeetup.json --parameters ParameterKey=ParamKeyName,ParameterValue=timohare+aws01@gmail.com ParameterKey=ParamSshCidr,ParameterValue=162.244.136.121/32
```

### Check the stack progress, either through the web console or on the command line
```
aws cloudformation describe-stacks
```

### To recreate it, first delete the current stack (or give the new stack a new name)
```
aws cloudformation delete-stack --stack-name <stack name>
```
My specific command line is
```
aws cloudformation delete-stack --stack-name arn:aws:cloudformation:us-west-2:810429055117:stack/seattle-aws-soln-arch-05/30173de0-f1bd-11e4-9b3b-50d5020578e0
```

### Log in to the Bastion
```
ssh-add -k [keyfilename.pem]
ssh -A ec2-user@[bastion public ip]
ssh ec2-user@[webserver private ip]
```


