# Getting Started 

- AWS : Leading market tool in industry. 
  
- Use cases : build scalable and sophisticated applications,  big data analytics , IT backup & storage.
  
- AWS is GLOBAL.
  
- AWS components : 
    - Regions 
    - Availability zones 
    - Data Centers
    - Edge Locations / Point of presence

- Each region is connected with a network.
- In each region -> you have availability zones.
  
- Concept of Regions : 
  - AWS has regions all around the world.
  - For example: us-east-1. eu-west-3 , etc
  - A region is a cluster of data centers.
  - Most AWS services are region-scoped.
  - Not all regions have all services.

- How to choose an AWS REGION ?
    - Compliance :
    - Proximity :
    - Available Services : 
    - Pricing :
  
- Concept of Availability Zones (AZ): 
    - Each region has many availability zones.
    - (minimum : 3 and maximum : 6)
    - Example : Region: ap-southeast-2
      - It have Availability Zones :  ap-southeast-2a , ap-southeast-2b , ap-southeast-2c 
      - Now each of AZ is one or more discrete data centers with redundant power , networking , connectivity.
      - AWS does not tell how many data centers are present in the AZ.
      - These AZ are separated from each other so that they are isolated from diasters.
      - AZ are inter-connected with high bandwidth and low latency thus forming a region. 

- Concept Of Point of Presence (Edge Location):
    - 400+ Point of Presence in 90+ cities across 40+ countries.
    - Content is delivered to end users with lower latency.

- Example of aws global services : 
    - IAM , Route 53 , CloudFront (CDN) , WAF(web application firewall)
  
- Most AWS services are Region scoped:
  - EC2 (IaaS)
  - Elastic Beanstalk (PaaS)
  - Lambda (FaaS)

- TIP : choose the region that is closest to your location.

- Route 53 : does not require region. It is a global service.
