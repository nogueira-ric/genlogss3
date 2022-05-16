# Streaming Pipeline using Kinesis

## Tools that were used:

> AWS EC2 - running Ubuntu 18.04

> Logrotate

> AWS Kinesis Data Firehose Delivery Streams

> Boto3

> Jupiter Lab

Install logrotate and nginx

sudo apt-get install logrotate

Install nginx as well.

sudo apt-get install nginx

The config files are the /etc/logrotate.d/

Issue the command ls-ltr /etc/logrotate.d/ to see the file on it.

> Enter the access-log file path in logrotate configuration.

>/path/access.log {

        su ubuntu ubuntu # If you use another distribution, check the user.
        start 1
        daily
        rotate 100
        compress
        copytruncate

}

Issue this command to force files rotating.
sudo logrotate /etc/logrotate.d/gen_logs

In case of the log is not rotating, so you can force it by issuing the command sudo logrotate -f /etc/logrotate.d/gen_logs

Add the logrotate on crond typing the command crontab -e


## Installing Kinesis Firehouse Agent.

Installing Kinesis Firehose agent on Linux, look up to the AWS docs download and install the agent at:
https://docs.aws.amazon.com/firehose/latest/dev/writing-with-agents.html

Use the github files from the link https://github.com/awslabs/amazon-kinesis-agent then transfer the files to the folder has just created.

Kinesis Firehouse has to be configured as the source = PUT and destination S3 must also be informed.

Edit the agent.json file located on /etc/aws-kinesis/
This is the default settings: You can follow the instruction to set the credentials on https://docs.aws.amazon.com/firehose/latest/dev/writing-with-agents.html#agent-config-settings

Restarting aws-kinesis agent and checking the aws-kinesis-agent status to be sure it’s running.

##  Customizing s3 folder using Kinesis Delivery Stream

You may want the logs to be stored in bucket S3 in the form year=XXXX/month=XX/day=XX

To perform the configuration you must create a prefix and include the following namespace timestamp in the following format:

Prefix: myPrefix/year=!{timestamp:yyyy}/month=!{timestamp:MM}/day=!{timestamp:dd}/

For reference follow the link below:
https://docs.aws.amazon.com/firehose/latest/dev/s3-prefixes.html

Check if the logs are being generated in the informed format.

You can use the Jupyter Lab notebook to run the codes and access the S3 bucket.