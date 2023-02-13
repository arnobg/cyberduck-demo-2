# cyberduck-demo-2

Task:

I'd like the candidate to make this xml file (attached to this email) accessible on a public URL. Assume that this xml file will be consumed by a web service. Please consider best practice: backups, availability, monitoring, logging, etc.

Solution:

This project allows the creation of a s3 bucket where the xml file will be hosted, with Cloudfront as the CDN, without ACM configurations. This is useful when you want to host files, or a website, over a CDN but don't necessarily need a domain name. 
For simplicity reasons, as this task involves a single file, I have not used the bucket to act as a static website, but that can be appended easily if the requirement changes. Along with the same, we can also use custom domain names along with certificate manager.

Optionally I have added some best practise features which can be setup for this project. Easy option to pass your AWS credentials can be to configure AWS CLI on the workstation and run the project.

Enabled access logging for the primary bucket and Cloudfront.
For monitoring, configured CloudWatch alarms using CloudFront metrics and further used SNS topics for Alerting based on Requests
Configured AWS Backup to backup the xml file stored in the S3 bucket
Configured custom ACLs for the buckets
Enabled Cross Region Replication of buckets for higher availabilty incase there is a regional outage.
Enabled versioning on primary and replication buckets.
Enabled lifecycle events for the primary and replication buckets, to archive and eventually delete versioned data.


Please note, while I have tried to follow the best practices out-of-the-box, there are still some recommended setup which can be added further. Few of those can be - 
We can consider creating a WAF (Web application Firewall) in front of the cloudfront distribution. It is highly recommended that you use one, especially in a production environment. 
We can also configure the CloudFront distribution to add the Geo Restriction feature (Geo Blocking), thereby ensuring we can blacklist/whitelist requests only from specific countries.
We can enable the default S3 SSE encryption for the buckets and ensure replication takes place along with encryption.
We can also enable failover on Cloudfront to use the replication bucket whenever an error occurs on the primary region.

