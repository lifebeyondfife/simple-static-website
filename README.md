# Simple Static Website
Create a simple, cheap, CDN backed, static website using a single AWS CloudFormation script. Perfect for sites built using static site generators e.g. Gatsby, Hugo, 11ty; stateless React apps; or just plain old HTML, CSS, and image files.

## Instructions
1. Register a domain in AWS [here](https://console.aws.amazon.com/route53/home#DomainListing:)
1. Created a Hosted Zone for that domain in [Route53](https://console.aws.amazon.com/route53/v2/hostedzones#)
1. Create a new [CloudFormation stack](https://console.aws.amazon.com/cloudformation/home?region=us-east-1) using the `simple-static-website.yaml` template. This *MUST* be done in `us-east-1` owing to constraints with CloudFront.
1. Provide the parameters:
    * DomainName
    * WebsiteName
    * HostedZoneId (using the console, a list will be provided)
    * BucketName (Optional), if you want to use an existing bucket. CloudFormation will generate the bucket name from the URL subdomain, if left empty.
1. Provision the CloudFormation stack using the console or with awscli:

    ```
    aws cloudformation deploy \
        --stack-name foo \
        --template-file simple-static-website.yaml \
        --parameter-overrides \
            DomainName=example.com \
            HostedZoneId=ABCDEFGHIJK0123456789 \
            WebsiteName=www
    ```
1. Put a simple index.html file in the newly created [S3 bucket](https://s3.console.aws.amazon.com/s3/home). Check CloudFormation output of the stack for a sample awscli command.
1. Visit your new website at the domain you provided. See CloudFormation outputs for URL.

## A note on using a Content Distribution Network (CDN)
Remember that the CloudFront CDN will cache your website at several locations around the world. If you change your site, you will have to [invalidate the cache](https://www.simplified.guide/aws/cloudfront/invalidate-cache). Charges apply, but on the whole this is an extremely cheap setup because it doesn't run any servers.

## Acknowledgements
This script was inspired by [Alain Seng's excellent blog post](https://medium.com/@Al-un/aws-cloudformation-https-static-website-s3-route53-cloudfront-438090157c1f), as well as the output of my existing manually provisioned sites run through Amazon's now defunct [CloudFormer template](https://web.archive.org/web/20191203150607/https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-using-cloudformer.html). CloudFormer is an excellent tool, however, it has been swept under the carpet by Amazon owing to the increasing number of CVEs the solution left users open to. There's a good write up by [karimelmel](https://github.com/karimelmel) about this [here](https://blog.karims.cloud/2020/09/25/cloudformer-review-part-1.html). Thanks to [eisenhowerj](https://github.com/eisenhowerj) for improving my CloudFormation script, and adding new features.
