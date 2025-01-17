<!-- PROJECT LOGO -->
<div align="center">

<h2 align="center">AWS SAM S3 Report template</h3>

  <p align="center">
    An easy and simple step by step guidelines
  </p>
</div>

<!-- GETTING STARTED -->
## Introduction
### Description
* Create a SAM template to deploy the lambda function listening to HTTP request and log it into S3 bucket.

### Tech stack

* Programming Language: Typescript
* Framework: NodeJS 20
* SAM CLI

## Step by step guidelines
1. Install SAM CLI
2. Run sam init and choose appropriate template
3. Run sam build --debug && sam deploy --guided
4. Grand permissions
5. Add business logic to the lambda handler function

### Experiences
- Use SAM build-in template.yaml file to avoid bugs that take a lot of time to fix
- Put the template.yaml, samconfig.toml, package.json and typescript entry point in the same directory
- Add "deploy": "sam build --debug && sam deploy --s3-bucket <S3-bucket-name> --guided" into "script" key of the package.json file then run npm run deploy for more convenience
- Specify the bucket name in the sam deploy command would help you avoid a lot of bugs
- When you need to add libraries to the lambda function there are 2 ways:
  * Create .npmrc file, add production=true. All the dependencies will be deployed with the lambda function
  * Add layers to template.yaml, the snippet would be similar to below:
    ```bash 
      Json2CsvLayer:
      Type: AWS::Serverless::LayerVersion
      Properties:
      LayerName: json2csv-layer
      Description: Common dependencies
      ContentUri: layers/json2csv
      CompatibleRuntimes:
        - nodejs18.x
      LicenseInfo: 'MIT'
      RetentionPolicy: Retain
    ```
