PROJECT NAME: "SNS NOTIFICATION ON S3 EVENTS”

AWS SNS: Amazon Simple Notification Service (SNS): A fully managed messaging service provided by AWS, allowing the distribution of messages to a variety of endpoints or clients
Uses: Simple Notification Service (SNS) is used for sending messages or notifications across different services. It acts like a messenger, ensuring information reaches various parts of your AWS applications. SNS is handy for notifying about events, coordinating between services, and facilitating communication in a scalable and flexible manner.
In this project, I set up an Amazon SNS topic and created a subscription to receive email alerts. I configured an S3 bucket to send event notifications to the SNS topic. After editing topic access policies, I uploaded a sample file to the S3 bucket, triggering an SNS notification to my email, successfully demonstrating end-to-end event-driven communication. 
Step 1: Create an SNS Topic
1. Navigate to the SNS service.
2. Click on "Topics" and then select "Create Topic."
3. Choose "Standard" as the topic type.
4. Provide a name of your choice.
5. Leave all other settings as default and scroll down.
6. Click on "Create Topic."

Step 2: Create a Subscription
1. Click on "Create Subscription."
2. Choose the protocol as "Email."
3. Enter your email address as the endpoint.
4. Click on "Create."
5. Check your email inbox, refresh, and confirm the subscription.


Before moving to step 3 
create a sample bucket in AWS S3, it will be useful in next steps 
Step 3: Edit SNS Topic and Set policy
1. Navigate back to your SNS topic.
2. Click on "Edit" and scroll down to the "Access Policy" section.
3. Replace the default policy with the provided example policy.
4. Replace the topic ARN with your topic ARN.
5. Replace the source ARN with the S3 bucket ARN.
6. Replace the source account with your account ID.
7. Click on "Save Changes."
ACCESS POLICY 
#Policy:
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
"Resource": "SNS-topic-ARN", (copy ARN from topic)
"Condition": {
"ArnLike": {
"aws:SourceArn": "arn:aws:s3:*:*:bucket-name"(copy ARN from s3 bucket)
},
"StringEquals": {
"aws:SourceAccount": "bucket-owner-account-id"(provide aws account ID)
}
}
}
]
}

Step 4: Configure S3 Bucket Event Notification
1. Go back to your S3 bucket.
2. Go to properties and scroll down to "Event Notifications."
3. Select "Create Notification."
4. Provide a name for the event.
5. Choose "All object create events."
6. Select "SNS Topic" as the destination.
7. Choose your SNS topic for the SNS Topic field.
8. Click "Save."
Step 5: Test the Configuration
1. Upload a test file to the S3 bucket.
2. Verify that you receive a notification.

