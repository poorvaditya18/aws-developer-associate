# IAM : IDENTITY AND ACCESS MANAGEMENT

- IAM : Identity and Access Management
- it is a global service
- here we are going to create users and assign them to a group.
- ROOT account created by default shouldn't be used or shared.
- Create : Users --> one user represents one person within organization.

  - Therefore, Users can be grouped.
  - Suppose :

  1. Alice , Bob , Charles --> group : Developers
  2. David , Edward --> group : Operations
  3. Charles , David --> can be clubbed in another group based on functionality or use case --> Audit Team.

- [NOTE] : Groups only contains users not other groups. Users dont have to necessarily belong to a group and user can belong to multiple groups.

- Why do we create users and groups ?

  - To allow using AWS account and give them permission.
  - [IMP] : Users or Groups can be assigned JSON documents called policies or IAM policies.
  - These policies define the permissions of the users. (what things or actions users can perform)
  - [PRACTISE] : In AWS, you apply the least privilege principle : don't give more permissions than a user needs.

- Creating Users:

  - Dont use the root account.
  - IAM > Users > Create Users
  - provide user name
  - select provide access if you want to give access to the management console.
  - select I want to create an IAM user.
  - select Custom Password
  - Click Next
  - give permissions to the user
    - you can add directly as well as if you dont have group you can create it.
    - Give group name : admin
    - provide policy name
  - Now, add the user to the admin group.
  - Review and create
  - You can also provide tags : tags are used for metadata description.
  - create user.
  - check users list.
  - you can also see user groups. : admin
  - So, currently admin have one user in it.
  - If you see permission of admin , there is a administratorPolicy permission attached to the group admin.
  - Now user also have adminstratiorPolicy permission attached to it but it is attached via the group admin. That means user inherits the policy of the group admin.

- you can provide alias to the sign-in url.
- Now, sign-in to console using you IAM account-id and password.

- Concept of IAM POLICIES :

  - If you set the policy in group . Users in that will inherit all the policies associated with that group.
  - INLINE POLICY is attached to that user who does not belong to any group.
  - A user can have multiple policies attached to it. Basically , it will inherit all the policies associated with the group it belongs to.

- IAM : POLICY STRUCTURE

  - Consists of :
    - "Version" : policy language version
    - "Id" : an identifier for the policy (optional)
    - "Statement": one or more individual statements (required)
      - "Sid" : identifier for the statement (optional)
      - "Effect" : whether the statement allows or denies access (Allow, Deny)
      - "Principle" : which account/user/role to which this policy applied to
      - "Action" : list of actions this policy allows or denies
      - "Resource" : list of resources to which the actions applied to
      - "Condition" : conditions for whent this policy is in effect (optional)

- IAM : Policy

  - we can add permissions directly or give inline policy
  - Suppose policy : `AdministorAccess`, it will look something like this :
    `      {
    "Version":"2012-10-17",
    "Statement":[
        {
            "Effect":"Allow",
            "Action":"*",
            "Resource":"*",
        }
    ]
}`
  - `*` -> denotes all access
  - `Get*` -> means anything starts with start you have access for it.
  - You can create your custom IAM policy.

- IAM : Password Policy

  - Strong password = higher security
  - In AWS , you can setup a password policy

    - minimum password length
    - Require Specific character types
      - including uppercase letters
      - lowercase letters
      - numbers
      - non-aplhanumeric characters
    - Allow all IAM users to change their own passwords
    - Require users to change their password after some time (expiry period)
    - prevent password re-use

    - MFA ( multi-factor authentication)

      - Users have access to account and can possible change config
      - You want to protect your root account and IAM users
      - MFA = password you know + security device you own
      - example : Alice ( password + MFA) => sucessful login
      - MFA Devices option :
        - Virtual MFA device (Google Authenticator (phone-only), Authy(multi-device))
      - Universal 2nd Factor security key (physical device) , etc

    - setting up password policy
      - IAM > account settings > edit
      - choose IAM default or custom (as per usecase)
      - go to security credentials
      - check whether you are login using root user or not
      - Protect your root user using MFA

- How can users access AWS ?

  - To access AWS you have 3 different options :

    1. AWS management console ( password + MFA )
    2. AWS CLI : protected by access keys
    3. AWS SDK : for code protected by access keys

  - Access keys are generated through AWS console.
  - Users manage their own access keys.
  - Access keys are secret , just like a password. DONT SHARE.
  - Access Key ID ~ username
  - Secret Access Key ID ~ password

  - AWS CLI : interact with AWS services using commands in your command line interface. - Direct access to the public API of aws services - You can develop scripts to manage your resources - open-source - alternative to using management console.

  - AWS SDK : software development kit - Language-specific API's - enables you to access and manage aws services programmatically - embedded within application

- USING AWS CLI :

  - `aws configure`

    - provide access key and secret access key
    - provide default region and default output format

  - `aws iam list-users` : will lists all the users in the account.

  - CLI permissions are same as the management console permission that you set.

- AWS CLOUD SHELL :

  - terminal in the cloud of aws.
  - this will return the same output as if you are using on the local pc.
  - all the files that you are creating the cloud shell will persists even if you restart.
  - You can download/upload files to cloud shell terminal.

- IAM : Roles

  - we will assign permissions to aws services with IAM roles
  - For example : EC2 instance --> may want to perform some action on aws therefore we will setup permission for this ec2 using ec2 instance roles.
  - IAM > Role > selec trusted entity > select services > add permissions (policy) > provide role name , details , description > finally create it.

- IAM : Security Tools

  - IAM Credentials Report (account-level) : all account users and the status of their various credentials
  - IAM Access Advisor (user-level) : shows the service permissions granted to user and when those services were last accessed.

- IAM : Best Practices
  - Dont use root account except for AWS account setup
  - One physical user = One AWS user
  - Assign users to groups and assign permissions to groups
  - Create strong password policy
  - Use and enforce MFA
  - Create and use Roles for giving permissions to AWS services
  - Use Access Keys to access AWS programmtically
  - Audit permissions of your account using IAM credentials report & IAM Access Advisor
  - Never share IAM users and access keys

