# AWS IAM

* [The Code Spaces Nightmare](http://blog.trendmicro.com/the-code-spaces-nightmare/)
* [git-secrets](https://github.com/awslabs/git-secrets)

User can have an account with password, but can't perform any function without being inside a Group that grant permission.

Authentication is handled by Users and Groups, whereas authorization is handled by IAM policies.

The idea behind IAM is to separate users and groups from the actions they need to perform.

## Least Privilege

You have to earn your privileges! Start with the absolute minimum.

## Shared Security Model



## Users

* Individual credential
* Can have many groups

```
▶ aws iam create-user --user-name mech
▶ aws iam create-access-key --user-name mech

▶ aws iam put-user-policy --user-name mech --policy-name db-backups --policy-document file://./s3-policy.json
▶ aws iam get-user-policy --user-name mech --policy-name db-backups
```

Because Users and Groups need to deal only with authentication, they are relatively simple. If you're familiar with how Unix or Windows handles user and group permissions, you already know the core principles behind IAM Users and Groups.

To ease administration, users can be placed in groups. When an IAM policy is assigned to a group, all members of that group inherit the permissions designated by the IAM policy. It is not possible to nest groups.

Assigning permissions to specific users has its purposes, but it is often a sign that tasks and knowledge are not being shared across the team. If Alice is the only person with `CreateSnapshot` permissions, how is Bob going to handle backups while she is on vacation?

Aim to map AWS groups to specific roles within your organization, and apply the policy to the group instead.

## Groups

* Easier to assign the same permissions to multiple users
* Simpler to re-assign permissions based on change in responsibilities
* Only one change to update permissions for multiple users
* Create group according to business function

If you have more users, you do not want to grant those users access to resources individually, that will be too tedious and time consuming. Instead we use a Group to cover all users with similar access rights and permissions.

Users inherit permissions from a group.

## Roles

The best way to protect credentials is to not need them in the first place. That's where IAM Roles come into play.

How is Roles different from Groups? When you want a user to "assume" a role. The user can switch role and once done with the things will switch back to their original role.

A user can be under one group but have many different roles.

More for EC2 user to access other AWS services like RDS database.

* Roles are used to eliminate the need to bake credentials into AMIs.
* There is a downside to reusing the same keys for multiple roles: it becomes very difficult to change them because key need to be rotated often.
* Just like user but can't login. Only use to attach policies on.
* Alternate form of authentication
* Uses temporary credentials
* Role expires after 15 minutes?
* Automatic key rotation
* Cross-account access
* Attached to EC2 and access S3 storage
* Assign least privilege to the application
* `sts:AssumeRole`

If you do not want to embed credential to your Resource, you can make use of role as an alternative.

## Policies

Collection of permissions. You can apply policies to user, group, roles, etc. Policies are the foundation of it all.

1. Explicit Deny - If permission is denied by one of the policies, the request can be immediately denied.
2. Explicit Allow - If permission is explicitly granted, the request is allowed.
3. Implicit Deny - Finally, if permission was not explicitly granted, it is denied (a default deny)

**Note:** When conflicting permissions are encountered, `Deny` takes precedence over `Allow`.

**Being explicit is better than being implicit.** So try not to use `NotResource`, `NotAction` or `NotPrincipal` variants.

## Key Rotation

```
▶ aws iam generate-credential-report
▶ aws iam get-credential-report | jq -r '.Content' | base64 -D > report.csv
```