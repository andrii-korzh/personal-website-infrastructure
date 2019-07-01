# Website infrastructure
Website infrastructure

## Example of script that can be used for deploy
```
#!/usr/bin/env bash

TEMPLATE=main.yaml
OUTPUT_TEMPLATE=packaged.yaml
STACK=$1
S3_DEPLOY_BUCKET=$2

GitHubOwner=$3
GitHubSecret=$4
GitHubOAuthToken=$5
DistributionId=AKDistribution
DomainName=andrii-korzh.com
BranchName=prototype
RepositoryName=personal-website

aws cloudformation package \
  --template-file $TEMPLATE \
  --s3-bucket $S3_DEPLOY_BUCKET \
  --output-template-file $OUTPUT_TEMPLATE

aws cloudformation deploy \
  --template-file $OUTPUT_TEMPLATE \
  --capabilities CAPABILITY_IAM \
  --stack-name $STACK \
  --parameter-overrides \
  DistributionId=$DistributionId \
  DomainName=$DomainName \
  BranchName=$BranchName \
  RepositoryName=$RepositoryName \
  GitHubOwner=$GitHubOwner \
  GitHubSecret=$GitHubSecret \
  GitHubOAuthToken=$GitHubOAuthToken
```
