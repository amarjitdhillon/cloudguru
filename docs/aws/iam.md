# IAM 🔑
- IAM is universal service and it does not apply to a single region; it is cross-region.
- The `root account` is the account created for the first time and it has full access (also called as God mode 🧚 ).
- New users have no permissions when created 
- Access key id and secret access key are required for programmatic access to AWS. They can’t be used to login to the console.
- Use MFA in the root account. We can use the Google Auth app for this 📱
-  IAM is concerned with the raw AWS resources, not access to running web applications.

!!! tip
    Setting up a cross-account IAM role is currently the only method that will allow IAM users to access cross-account S3 buckets both programmatically and via the AWS console.

## Types of policies in IAM
There are four types of policies in IAM:-

- Identity-based
- Resource-based
- Organization SCPs
- Access control lists (ACLs)

You can provide console access and programmatic access via IAM. Programmatic access includes API and CLI access.

!!! remember 
    - IAM is not the managed service for handling MFA Delete setup on S3 buckets
    - Users, groups, roles, permissions, and similar constructs are part of IAM
    - Organizations and organizational units are part of AWS Organizations, a different facility.
    - User policies are not part of IAM but permissions are.
    - IAM policies are written in JSON.
    - IAM policies can be attached to users, groups, and roles in the case of identity-based policies, and AWS services and components via resource-based policies.
    - Restoring revoked permissions for a user and changing the support options need the root user access.
    - IAM changes apply immediately to all users across the system; there is no lag, and no need to log out and back in.
    - ==Power-user access is a predefined policy that allows access to all AWS services with the exception of group or user management within IAM==


!!! warning
    - AWS strongly recommends you delete your root user access keys and create IAM users for everyday use.
    - IAM root user account is needed for very privileged access; in this case, that’s creating a CloudFront key pair, which essentially provides signed access to applications and is a very trusted action.
    - AWS firmly believes that root account access should be highly limited, but also not confined to a single user. Having a very small group of engineers (ideally AWS certified) is the best approach to reducing root account level access as much as possible.

- You will always need to provide `non-root sign-in URLs` for new users.
- **New users have no access to AWS services. They are “bare” or “empty” or “naked” users, as they can merely login to the AWS console (if a URL is provided). They cannot make any changes to AWS services or even view services.**
- AWS usernames have to be unique across the AWS account in which that user exists 🔑
- ==If you have an external Active Directory, you’d want to federate those users into AWS. This allows you to use the existing user base, not re-create each individual user.==