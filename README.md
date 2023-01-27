PetIDF is a serverless application that uses web idententity federation to allow anyone with a google account to access very imporant cat photos in a private S3 Bucket without having an AWS account with correct credentials.

Apply the CloudFormation template which implements a CFN Stack that creates a private S3 Bucket full of cat photos, the application S3 Bucket, and the CloudFront distribution. It also creates a Lambda Function that copies objects into the buckets.
![Screenshot_1](https://user-images.githubusercontent.com/109190196/214977753-c4a7cbc8-99de-4494-abf7-653c6a8c62e6.jpg)

Configure a Google API Project with credentials for the serverless application to interact with the Google API.
![Screenshot_2](https://user-images.githubusercontent.com/109190196/214977955-777814fd-5e42-4b8c-8c81-1de74da37c85.jpg)

Create a new identity pool in Cognito that allows authentication from Google by inputting your Google Client ID. Create a new IAM Role for authenticated users so Cognito has the ability to access the correct AWS Resources. Attach another permissions policy that allows Cognito to access the private S3 Bucket full of cat photos. When the serverless application receives a Google authentication token, it provides the token to Cognito. Cognito then assumes a role and generates temporary security credentials.
![InkedScreenshot_3](https://user-images.githubusercontent.com/109190196/214978042-8f83f47f-288f-43ac-8a42-f7f8b5c4c50a.jpg)
![Screenshot_4](https://user-images.githubusercontent.com/109190196/214978102-63ca3332-a518-4db0-807a-5aa04c65e1d5.jpg)
![Screenshot_5](https://user-images.githubusercontent.com/109190196/214978122-5e82532b-5443-4360-a2e2-5a003df8497b.jpg)

Update the index.html file located in the application S3 Bucket to use your Google Client ID. Update the scripts.js file with the Cognito Identity Pool ID & Private S3 Bucket name. Upload the updated files into the application S3 Bucket.
![Screenshot_6](https://user-images.githubusercontent.com/109190196/214978136-3c969816-bebc-4bc2-bc12-75762ca95f48.jpg)

Go to CloudFront and open the application in your browser with the distribution domain name. Sign into Google with your Google account. This will create a Google Authentication Token which Cognito will exchange for temporary AWS credentials. The images in the private S3 Bucket full of cat photos will be shown via presignedURL.
![Screenshot_7](https://user-images.githubusercontent.com/109190196/214978173-c16e6361-7032-4281-8880-da831551a1ce.jpg)
![InkedScreenshot_8](https://user-images.githubusercontent.com/109190196/214978368-7ccd000d-344d-457b-b356-64e2e60ee14c.jpg)
