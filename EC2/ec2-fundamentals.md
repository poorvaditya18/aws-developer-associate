# EC2 Fundamentals

## Setting up Alarm Budget :

    - Root account > Go to Billing and Cost Management > Iam user and role access to billing information > enable it .
    - Users that are administrators will have billing access.
    - Navigate to charge by Service and check your bill breakdown.
    - setting budget
      - Budgets >  Use a template (simplified) > Zero spend budget > give budget name > add email > create it.
      - You can use different templates like monthly cost budget.

## EC2 Fundamentals :

    - EC2 = Elastic Compute Cloud = IaaS
    - It mainly consits in the capability of :
      - Renting virtual machines (EC2)
      - Storing data on virtual drives (EBS)
      - Distributing load accross machines (ELB)
      - Scaling the services using an auto-scaling group (ASG)

    - EC2 sizing & config options :
      - OS : linux , windows , macos
      - How much compute power and cores (CPU)
      - How much RAM
      - How much storage space :
        - attached through network (EBS & EFS)
        - or hardware attached (EC2 instance store)
      - Network Card : speed of the card , PUBLIC IP
      - Firewalls rules : security rules
      - Bootstrap script (config at first launch): EC2 user Data

    - EC2 user data :
      - bootstrap our instances using user data script
      - bootstrapping means launching commands when a machine starts
      - script is only run once at the instance first start. This scripts runs with the root user i.e it have sudo rights.
      - EC2 user data script helps to automate boot tasks such as :
        - Install updates , softwares
        - Download common files
        - anything that suits your usecase

      - Example of ec2 instances:
        - t2.micro (part of aws free tier upto 750 hours per month)
        - t2.xlarge

## Creating EC2 instance using EC2 User data

    - EC2 > INSTANCES > LAUNCH INSTANCES
    - give instance name
    - select base image (operating system) :  prefer ubuntu
    - select > architecture 64-bit(x86)
    - select > Instance type : t2.micro
    - setup and create : key-pair(login)
      - give key-pair name
      - select key-pair type : RSA encrypted gives private and public key pair
      - Private key file format :
        - .pem : if you have mac , linux ,windows v10
        - .ppk : windowsVersion < v10
    - Network settings :
      - Instance will auto assign public ip
      - security group will be created and it is used to connect to our ec2 instance called 'launch-wizard-1'.
        - Allow SSH traffic from `Anywhere`
        - Allow HTTP traffic from Internet
      - Configure Storage
        - Advance you can configure EBS Volumes. By default : delete on termination is set to YES . When you terminate your instance it will delete your storage volume.
     - Advance details
       - At the bottom you have USER DATA here you pass the script.
     - Finally , launch instance


    - You will see instance details :
     - instane will be running
     - instance will have instanceId
     - public IPv4 to access the instance from internet . if you stop and restart public IPv4 will be changed .
     - private IPv4 access instance internally from aws. But private IPv4 will not be changed when you restart your instance.
     - instance type : t2.micro

## EC2 instance types :

1. General Purpose -> use case : greate for diversity such as web servers or code repositories. Balance btw compute , memory , networking.
2. Compute Optimized -> use case : that require high performance processor usecase batch processing , high performance web server , machine learning , gaming servers , media transcoding.
3. Memory Optimized -> use case : process large datasets in memory. High performance relational and non-relational databases , web scale cache stores , in-memory databases.
4. Accelerated Optimized
5. Storage Optimized -> use case : that require high , sequential read and write access to large data sets on local storage, High Frequency online transaction processing (OLTP) systems.
6. Instance Features
7. Measuring Instance performance

- Naming convention : m5.2xlarge
- m : instance class
- 5 : generation of the instance
- 2xlarge : size within the instance class

## Security Groups :

    - are acting as a "firewall" on EC2 instances.
    - Control how traffic is allowed into or out of our EC2 instances.
    - Only contain allow rules
    - Rules can reference by IP or by security group
    - Example :
             Inbound traffic
      -  www ---------------> [ SecurityGroup
             <--------------- EC2 instance ]
             Outbound traffic

    - They regulate:
      - Acces to PORTS
      - Authorised IP ranges - IPv4 and IPv6
      - Control of inbound network (from other to the instance)
      - Control of outbound network (from the instance to other)


    - can be attached to multiple instances
    - Locked down to a region/VPC combination
    - Does live "outside" the EC2 - if traffic is blocked the ec2 instance wont see it
    - good to maintain one separate security group for SSH access
    - [NOTE] : your application is not accessible (timed out) -> EC2 security group issue
    - [NOTE] : your application gives "connection refused" --> then it's an application error or it's not launched
    - BY DEFAULT , ALL INBOUND TRAFFIC IS BLOCKED
    - BY DEFAULT , ALL OUTBOUND TRAFFIC IS AUTHORISED.

## COMMON PORTS

    1. 22 = SSH -> Log into a linux instance
    2. 21 = FTP -> upload files into a file share
    3. 22 = SFTP (secured File transfer protocol) -> uploading files using SSH
    4. 80 = HTTP -> access unsecured websites
    5. 443 = HTPPS -> access secured websites
    6. 3389 = RDP (remote desktop protocol) -> log into a Windows instance

- [NOTE] : never ever configure your access key id and secret key id in EC2 instance. Because user might directly connect to the ec2 server and fetch your credentials. ----> USE IAM ROLES

- Good practise ! ==> Instance > select instance> actions > Go to security > modify IAM roles > choose your IAM role.

## EC2 Instance Purchasing Options :

    - Reserved Plan:
      - Reserved Instances ( 1 & 3 years term) - long workloads
      - Convertible Reserved Instances - flexible instances

    - Saving Plans: commitment to an amt of usage ,long workloads
    - Spot Instances
    - Dedicated Hosts
    - Dedicated Instances
    - Capacity Reservations

    - Ec2 on Demand:
      - Pay for what you use
      - Has the highes cost but no upfront payment
      - No long-term commitment

    - Ec2 Reserved instances :
      - 72% discount
      - reserve a specific instance attributes
      - Reservation period
      - Recommended for steady state usage applications

    `RESORT ANALOGY`
    - Which purchasing option is right for me ?
      - On demand :  coming and staying in resort wherver we like , we pay the full price
      - Reserved : planning ahead and plan to stay for a long time then you'll get good discount
      - Savings Plan: pay a certain amt per hour for certian period and stay in any room type
      - Spot instances : hotel allow people to bid for empty rooms and highest bidder keeps the room you can get kicked out at any time.
      - Dedicated Hosts : we book an entire building of the resort
      - Capacity Reservation : you book a room for a period with full price even if you dont stay
