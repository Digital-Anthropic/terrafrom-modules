
# AWS S3 Bucket && CloudFront && Lambda Egde Function

In this section we will cover up all documentation about how the modules
S3 Bucket, CloudFront, Lambda Function works, what resources creates and how to
use them.

## Terraform S3 Cloudfront Module

This module is designed to create all necessary resources regarding AWS S3 and
CloudFront to host a static website. We will list the resources below:

### S3 CloudFront Resources

| Name | Type |
|------|------|
| [aws_cloudfront_distribution.mkdocs_distribution](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudfront_distribution)| resource |
| [aws_cloudfront_origin_access_identity.access_identity](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudfront_origin_access_identity) | resource |
| [aws_s3_bucket.mkdocs_bucket](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket) | resource |
| [aws_s3_bucket_policy.allow_access_from_cloudfront](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_policy) | resource |
| [aws_s3_bucket_website_configuration.mkdocs_website](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_website_configuration) | resource |

### How to use

You can create an S3 Bucket associated with a CloudFront by using the
'locals.tf' file. Below is an example how to use `locals.tf`.

```hcl
locals {
    terraform_s3_cloudfront_lambda_func = {
      
    "mkdocs-bucket" = {
      bucket_name               = "mkdocs-bucket"

    }

    "bucket-for-modules" = {
      bucket_name               = "bucket-for-modules"

    }

    "new_bucket" = {
      bucket_name               = "new_bucket"

    }
}
}
```

Change "new_bucket" instance name and bucket_name with the one desired. Save the
changes, commit and push. Now you have brand new bucket by default associated
with Cloudfront and Lambda Function.

*Note*: You can add how many buckets you wish.

## Lambda Edge module

This module is designed especially for using in combination with S3 Cloudfront
module. The Lambda function perse it used to resolve the URI paths for index
redirect.

*Note*: The CloudFront is automatically associated with the lambda function
after creation of the bucket.

### Lambda Resources

| Name | Type |
|------|------|
| [aws_iam_role.lambda_execution](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role_policy.lambda_execution](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy) | resource |
| [aws_lambda_function.index_redirect](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lambda_function) | resource |
| [archive_file.index_redirect_zip](https://registry.terraform.io/providers/hashicorp/archive/latest/docs/data-sources/file) | data source |
