- It is a CDN which have 2 types of distributions
    1. `Web distribution`: for static and dynamic content, media files 
    1. `RTMP`: to speed up the distribution of streaming’s media files using the Adobe Flash’s RTMP (Real-Time Messaging Protocol) . Using this the user can begin playing - the file before it’s being downloaded from the server.
- `Origin` is the actual location where the resource is (it can be S3), `Edge` is where the user.
- Edge location will cache the data for some period of time called TTL(Time To Live)
- Distribution is the name given to the CDN, which is the collection of edge locations 💡
- You can clear the contents in the cache, but you will be charged for this.
- Invalidation removes the objects from the edge cache.
- `/*` will invalidate everything.
- Creating and deleting distribution takes some time.


!!! tips "Remember"
    - The invalidation API is the fastest way to remove a file or object, although it will typically incur additional costs.
    - First, remove the file from the origin servers; then set the expiration time on the CloudFront distribution to 0 in order to remove the file from the CloudFront.
    - RDS instance can be an origin server.
    - You can read and write objects directly to an edge location. You cannot delete or update them directly; only the CloudFront service can handle that.
    


CloudFront allows interaction via CloudFormation, the AWS CLI, the AWS console, the AWS CLI, the AWS APIs, and the various SDKs that AWS provides.

CloudFront can front a number of AWS services: AWS Shield, S3, ELBs (including ALBs), and EC2 instances.

CloudFront automatically provides AWS Shield (standard) to protect from DDoS, and it also can integrate with AWS WAF and AWS Shield advanced. These combine to secure content at the edge.

CloudFront is easy to set up and lets you create a global content delivery network without contracts. It’s also a mechanism for distributing content at low latency.

When you create a CloudFront distribution, you register a domain name for your static and dynamic content. This domain should then be used by clients.

There is no charge associated with data moving from any region to a CloudFront edge location.

CloudFront supports a variety of origin servers, including a non-AWS origin server. It supports EC2  regardless of region, as well. It does not support RDS or SNS.

Edge locations can be set to have a 0 second expiration period, which effectively means no caching occurs.

CloudFront is able to distribute content from an ELB, rather than directly interfacing with S3, and can do the same with a Route 53 recordset. These allow the content to come from multiple instances.

CloudFront serves content from origin servers, usually static files, and dynamic responses. These origin servers are often S3 buckets for static content and EC2 instances for dynamic content.

