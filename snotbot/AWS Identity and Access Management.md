Building blocks 
Policy


Intro to IAM
Also known as AWS IAM
Manage roles, user groups and policies
Roles are permissions for services
User groups are permissions for users
Policies are a set of permissions
Rule of least privilege





Snotbot
No user groups as we have no users
Roles:
Both Lambdas (SQS, Secrets Managers, SES)
Policies:
SES policy for custom permissions
SQS (sender and receiver Lambdas)



Thinking aobut IAM setting up
Think about permissions structure
Create policies to meet these permissions
Create roles and user groups
Assign policies to roles and user groups
Create users that fall under a user group
