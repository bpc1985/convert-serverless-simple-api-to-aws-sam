# CONVERT SEVERLESS WITH SIMPLE API TO AWS SAM

- npm install --save-dev serverless-sam
- Add serverless-sam to plugins of file serverless.yml
- serverless sam export --output ./sam-template.yml

Once you have exported the template, you can follow the standard procedure with the AWS CLI to deploy the service. First, the package command reads the generated templates, uploads the packaged functions to an S3 bucket for deployment, and generates an output template with the S3 links to the function packages.

$ aws s3 mb s3://hung-convert-serverless-to-aws-sam

$ aws cloudformation package \
    --template-file sam-template.yml \
    --s3-bucket hung-convert-serverless-to-aws-sam \
    --output-template-file packaged-template.yml

The next step is to deploy the output template from the package command:

$ aws cloudformation deploy \
    --template-file packaged-template.yml \
    --stack-name hung-serverless-to-aws-sam-stack \
    --capabilities CAPABILITY_IAM

Testing with Chrome extension: POSTMAN or ADVANCED REST CLIENT

In order to delete stack, using this command

$ aws cloudformation delete-stack \
    --stack-name hung-serverless-to-aws-sam-stack