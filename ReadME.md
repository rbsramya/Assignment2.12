Given a Lambda function that is triggered upon the creation of files in an S3 bucket, answer the following:
1.What is the purpose of the execution role on the Lambda function?

The execution role (IAM role) assigned to the Lambda function defines what AWS services and resources the function can access while executing.

For example:

If the Lambda reads from or writes to S3

Publishes to SNS

Writes logs to CloudWatch Logs

2.What is the purpose of the resource-based policy on the Lambda function?

The resource-based policy on the Lambda function controls who or what is allowed to invoke the function.

In this case,

The S3 bucket triggers the Lambda — so S3 needs permission to invoke the Lambda function.

That permission is defined in a resource-based policy on the Lambda function, allowing the S3 service principal (and specific bucket) to invoke it.


3.If the function is needed to upload a file into an S3 bucket, describe (i.e no need for the actual policies)
 
    1.What is the needed update on the execution role?
        The execution role must be updated to allow s3:PutObject on the target S3 bucket.

This lets the function write/upload files to the specified bucket (and optionally to a specific prefix or path).
 
      
    2.What is the new resource-based policy that needs to be added (if any)?

        No new resource-based policy is needed for the Lambda function to upload to S3.

        Why? Because the Lambda function is calling S3, not the other way around.

        Lambda only needs IAM permissions to act on S3, which are defined in its execution role, not in resource policies on Lambda.

        However:

        The S3 bucket itself may need a bucket policy that allows the Lambda function’s role to write to it — especially if the bucket has strict policies.
 
     

