# AWS Lambda S3 Organizer

## Overview
This project automates the organization of objects uploaded to an Amazon S3 bucket using AWS Lambda and Python. When an object is uploaded, the Lambda function creates a folder inside the S3 bucket named after the current date and places the uploaded object within that folder.

## How It Works
1. A user uploads an object to the S3 bucket.
2. The AWS Lambda function is triggered by an S3 event.
3. The function retrieves the current date and creates a folder named as `YYYYMMDD/` inside the bucket (if it does not already exist).
4. The uploaded object is moved into the respective date-based folder.

## Prerequisites
- AWS account
- S3 bucket
- AWS Lambda with Python runtime
- IAM role with necessary permissions

## Setup Instructions
1. **Create an S3 Bucket**
   - Navigate to the AWS S3 Console.
   - Create a new S3 bucket or use an existing one.

2. **Create an IAM Role**
   - Go to the AWS IAM Console.
   - Create a new role with S3 and Lambda execution permissions.

3. **Create another s3 bucket**
   - upload the python script zip file to this s3 bucket.

4. **Deploy the Lambda Function**
   - Create a new AWS Lambda function.
   - Choose Python as the runtime.
   - Attach the IAM role created earlier.
   - Add S3 Put event triger to the Lambda. 
   - Upload the Python script from the s3 bucket

## Lambda Function Code (Python) is [here](https://github.com/li-zhang1/python-projects/tree/main/organize-s3-objects)


## Troubleshooting AWS Lambda Timeout Error

If you encounter the following error when you test the Lambda:

```
lambda got this error message: Response:
{
  "errorType": "Sandbox.Timedout",
  "errorMessage": "RequestId: 30915292-c683-4661-a8a3-5db8195a07aa Error: Task timed out after 3.00 seconds"
}
```

Follow these steps to resolve it:

### Steps to Increase Timeout in AWS Lambda
1. Go to **AWS Lambda Console**
2. Select your function
3. Click **Configuration** → **General configuration**
4. Increase the **Timeout** (e.g., set it to **10 seconds** or more as needed)
5. Click **Save**

This should resolve the timeout issue by giving your function more time to execute before being forcibly stopped.

## Testing
- Upload an object to the S3 bucket.
- Verify that the object is moved to a folder with today's date.
- Check AWS CloudWatch Logs for debugging information if needed.

## Notes
- Ensure the Lambda function has the correct IAM permissions (`s3:PutObject`, `AWSLambdaBasicExecutionRole`).
- The function runs automatically upon any upload event to the S3 bucket.

