# SNS-S3-AWS-Project
## Project Overview
This project demonstrates us the setup of Amazon Simple Notification Service (SNS) to receive notification alerts upon S3 bucket. The end to rnd driven communication invovles in creation of SNS topic and setting up subscription for alerts, configuring s3 event notification and testing the configuration.

## STEPS:

### Step 1: Create an SNS Topic
1. In the AWS cloud navigate to SNS service.
2. Click on "Topics" and then select "Create Topic."
3. Choose "standard" as topic type.
4. Give a name as of your own choice.
5. Remain the below settings as default and scroll down.
6. click on "Create Topic."

### Step 2: Create a Subscription 
1. Click on "Create Subscription."
2. Choose the protocol type as "email."
3. Provide your E-mail address to receive mail alerts as End-point.
4. Click on "Create"
5. Check your E-mail inbox refresh and confirm the subscription.

### Step 3: Edit SNS Topic and set policy 
1. Switch back to your SNS Topic.
2. Click on EDIT and keep scrolling down for the "Access Policy" section.
3. Replace the default policy with provided example policy from documentation.
4. Replace the ARN topic with your topic ARN.
5. Replace the source ARN with S3 Bucket ARN.
6. Replace the Source Account with your account ID.
7. Click on "save changes."

#### policy Example:
''' 
{
    "Version": "2012-10-17",
    "Id": "example-ID",
    "Statement": [
        {
            "Sid": "Example SNS topic policy",
            "Effect": "Allow",
            "Principal": {
                "Service": "s3.amazonaws.com"
            },
            "Action": [
                "SNS:Publish"
            ],
            "Resource": "SNS-topic-ARN",
            "Condition": {
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:s3:*:*:bucket-name"
                },
                "StringEquals": {
                    "aws:SourceAccount": "bucket-owner-account-id"
                }
            }
        }
    ]
} 
'''

### Step 4: Configure S3 Bucket Event Notification
1. Go Back to your S3 Bucket.
2. Navigate to properties and scroll down to "Event Notifications."
3. Select "Create Notification."
4. Provide a name for Event.
5. Choose "All object create events."
6. Select "SNS Topic" as destination.
7. Provide your SNS Topic which you have created in the SNS Topic field.
8. Click "SAVE"

### Step 5: Test the configuration 
1. Upload the test(or)sample file(or)document in your S3 Bucket.
2. Verify that you have receive a notification.
