# Simple Static Website
Create a simple, cheap, CDN backed, static website using a single AWS CloudFormation script. Perfect for sites built using static site generators e.g. Gatsby, Hugo, 11ty; stateless React apps; or just plain old HTML, CSS, and image files.

## Instructions
1. Register a domain in AWS [here](https://console.aws.amazon.com/route53/home#DomainListing:)
2. Created a Hosted Zone for that domain in [Route53](https://console.aws.amazon.com/route53/v2/hostedzones#)
3. Request an SSL certificate for that domain in [ACM](https://console.aws.amazon.com/acm/home)
4. Copy the ARN of the ACM certificate to your clipboard. It should have the format `arn:aws:acm:us-east-1:567800000000:certificate/1243abcd-xxxx-xxxx-xxxx-xxxxxxxxxxxx`
5. Create a new [CloudFormation stack](https://console.aws.amazon.com/cloudformation/home?region=us-east-1) using the `simple-static-website.json` template. This *MUST* be done in `us-east-1` owing to constraints with CloudFront.
6. Provide the three parameters: ACM arn, domain name for the website, Route53 hosted zone name
7. Provision the CloudFormation stack
8. Put a simple index.html file in the newly created [S3 bucket](https://s3.console.aws.amazon.com/s3/home)
9. Visit your new website at the domain you provided in step 6

## A note on using a Content Distribution Network (CDN)
Remember that the CloudFront CDN will cache your website at several locations around the world. If you change your site, you will have to [invalidate the cache](https://www.simplified.guide/aws/cloudfront/invalidate-cache). Charges apply, but on the whole this is an extremely cheap setup because it doesn't run any servers.

## Acknowledgements
This script was inspired by [Alain Seng's excellent blog post](https://medium.com/@Al-un/aws-cloudformation-https-static-website-s3-route53-cloudfront-438090157c1f), as well as the output of my existing manually provisioned sites run through Amazon's now defunct [CloudFormer template](https://web.archive.org/web/20191203150607/https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-using-cloudformer.html). CloudFormer is an excellent tool, however, it has been swept under the carpet by Amazon owing to the increasing number of CVEs the solution left users open to. There's a good write up by [karimelmel](https://github.com/karimelmel) about this [here](https://blog.karims.cloud/2020/09/25/cloudformer-review-part-1.html).
