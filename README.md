# Simple Static Website
Create a simple, cheap, CDN backed, static website using a single AWS CloudFormation script

## Instructions
1. Register a domain in AWS
2. Created a Hosted Zone for that domain in Route53
3. Request an SSL certificate for that domain in ACM
4. Copy the ARN of the ACM certificate to your clipboard. It should have the format rn:aws:acm:us-east-1:567800000000:certificate/1243abcd-xxxx-xxxx-xxxx-xxxxxxxxxxxx
5. Create a new CloudFormation stack using the `simple-static-website.json` template
6. Provide the three parameters: ACM arn, domain name for the website, Route53 hosted zone name
7. Provision the CloudFormation stack
8. Put a simple index.html file in the newly created S3 bucket
9. Visit your new website at the domain you provided in step 6

## A note on using a Content Distribution Network (CDN)
Remember that the CloudFront CDN will cache your website at several locations around the world. If you change your site, you will have to invalidate the cache. Charges apply, but on the whole this is a pretty cheap setup because it doesn't run any servers.

