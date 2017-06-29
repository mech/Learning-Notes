# AWS IAM

* [The Code Spaces Nightmare](http://blog.trendmicro.com/the-code-spaces-nightmare/)

User can have an account with password, but can't perform any function without being inside a Group that grant permission.

1. Implicit Deny - By default everything is implicitly disallowed
2. Explicit Deny - Then it look for all explicit deny which apply for all
3. Explicit Allow - Until you explicitly allow it

## Shared Security Model



## Users

## Groups

If you have more users, you do not want to grant those users access to resources individually, that will be too tedious and time consuming. Instead we use a Group to cover all users with similar access rights and permissions.

Users inherit permissions from a group.

## Roles

The best way to protect credentials is to not need them in the first place. That's where IAM Roles come into play.

How is Roles different from Groups? When you want a user to "assume" a role. The user can switch role and once done with the things will switch back to their original role.

A user can be under one group but have many different roles.

More for EC2 user to access other AWS services like RDS database.

* Alternate form of authentication
* Uses temporary credentials
* Role expires after 15 minutes?
* Cross-account access
* Attached to EC2 and access S3 storage

If you do not want to embed credential to your Resource, you can make use of role as an alternative.

## Policies

Collection of permissions. You can apply policies to user, group, roles, etc. Policies are the foundation of it all.