# Web-Identity-Federation
Apply the CloudFormation template which implements a CFN Stack that creates a private S3 Bucket full of cat photos, the application S3 Bucket, and the CloudFront distribution. It also creates a Lambda Function that copies objects into the buckets.

Configure a Google API Project with credentials for the serverless application to interact with the Google API.

Create a new identity pool in Cognito that allows authentication from Google by inputting your Google Client ID. Create a new IAM Role for authenticated users so Cognito has the ability to access the correct AWS Resources. Attach another permissions policy that allows Cognito to access the private S3 Bucket full of cat photos. When the serverless application receives a Google authentication token, it provides the token to Cognito. Cognito then assumes a role and generates temporary security credentials.

Update the index.html file located in the application S3 Bucket to use your Google Client ID. Update the scripts.js file with the Cognito Identity Pool ID & Private S3 Bucket name. Upload the updated files into the application S3 Bucket.

Go to CloudFront and open the application in your browser with the distribution domain name. Sign into Google with your Google account. This will create a Google Authentication Token which Cognito will exchange for temporary AWS credentials. The images in the private S3 Bucket full of cat photos will be shown via presignedURL.