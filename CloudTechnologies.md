# Cloud Fundamentals

## Load Balancers

- Multiple Application Web Servers to scale for traffic (horizontal scaling)
- Load balancer between users and webservers 
    - Intercepts traffic
    - Can be hardware or Software Defined
    - Bilateral communication (webserver says "I'm at 95%" -> LB redirects to another one)
    - Assigns traffic to different application servers

- What do they actually do ? 
- Usually 3 scenarios
    1. Dumb Server
        - Round-Robin
        - Each user: new server and then around mod
        - Quite not good, can be unbalanced over time as some users use more time 
    2. Application Server Load Aware Load Balancer
        - More configuration 
        - More expensive software
        - Best IF really needed
    3. Best Of Both Worlds
        - More control than RR, but less complicated than App.
        - 9 different algorithms to achieve that, random Select is one of them
    

## As A Service

- 3 main types: SaaS, PaaS, IaaS
- In levels of abstractions (stack):
    - Application    <- SaaS (persona: anyone)
    - Data
    - Runtime <- PaaS (persona: Dev) 
    - OS
    - Virtualization <- IaaS (persona: sysadmin)
    - Hardware
    
- If we use a car metaphor: 
    - IaaS: leasing
    - PaaS: renting
    - SaaS: taxi 

### SaaS

- Software as a Service
- Most common and most used
- Software over the internet 
- Via subscription model
- Highest level of abstraction

#### User access
- Muli-tenant architecture
    - Same software, same hosting 
    - Securely separated spaces for storing data
    - Pros:
        1. Cost efficient (no IT overhead cost, support because of subscription model)
        2. Scalability (horizontal or vertical: need more power/DB -> ask)
        3. Access anywhere (only need web browser, and that's it)
        4. Always the new version (version control, security issues, patches)


### IaaS

- Infrastructure as as Service
- Virtualized resources
- Usually 3 things:
    - Compute
    - Storage
    - Network (to hold together)

#### Compute
1. General Purpose Compute
    - Can be anything
    - Webserver
    - App Server

2. GPU 
    - Graphics Processor 
    - ML/AI

3. HPC
    - High Performance Computing
    - Frequency Requirements 
    - Lots of power

#### Storage

1. Object Storage
    - General storage
    - Relatively inexpensive
    - Pictures, Documents, etc  
    - Good archiving solution
    - Data/Graphics on webservers

2. Block Storage

3. File Storage

#### Network
- Needs to be dimensionned 
- How much data simultaneously (Gbps, Mbps ?)


#### Example for IaaS : AI workload
- 1B pictures in Object Storage
- Process to GPU server
- GPU doesn't have storage so stores in Block storage
- When finished: write back to object storage

### PaaS
- Platform as as Service
- Inherits IaaS but abstracts them away so the user doesn't have to worry about them
- In between

#### Pros: 
- Fast & Easy 
- Create/Delete apps (like for a conference)
- Cost effective
- Tools (DevApps, API Marketplaces) 

#### Cons: 
- Lack of control (can be a pro actually)
- Vendor Lock-in (hard to migrate from 1 cloud to another)
- Performance at scale can be an issue

## Microservices (vs Monoliths)
Monoliths pros:
- Easy to deploy
    
Monoliths cons: 
- Parts are highly dependent (ticketing company example)
- Language and framework bound (Java app -> Need Java)
- Growth : as the app gets larger, it's harder for the team to understand the principles
- Hero deployments (shut app and reup it )
- Scaling : needs to rescale everything (if payment part is overloaded for example)
        
Microservice:
- All independent
- Own container
- Communicate over API 
- Iterate at will/DevOps pipeline
    - Commit, Test, Push and we just upgraded
    - Worst case scenario: fail, well rest of the app still works
- Independent scaling
- "Every app function is it's own service"


## Public, Private, Hybrid Clouds

### Public Cloud
- Only pay for what you use
- Like a supermarket (idea of baking my own pie)
    - I will not grow the crops to do my own flour 
- Pick and chose what I want

Increasing Control, But increasing overhead (same principle as the hardware to application stack in Cloud Computing above): 
- Functions
- Containers (CloudFoundry)
- Orchestration (K8/OCP OpenShift)
- VPC (Virtual Private Cloud, like VMWare)
- BareMetal servers

#### Example
Imagine we have our legacy backend on baremetal servers. \\
We also have our frontend on top of Kubernetes orchestration.\\
What can we use in the cloud now; for storage (DB) for example: 
- Applications (Frontedn) use a SQL Store
- For our backend, we might need a cloud object storage
We can also use DevOps tools on the cloud:
- For the applications, we might have 2 sets of code:
    - One set for the app itself
    - One set for the infrastructure
    - Because we want to manage our infra as well
- We want to make use of some tool-chains capabilities
    - For the app, we use a toolchain which will deploy our containers
    - For the infra, we use a similar toolchain but we want to use TerraForm  
        - This will manage the worker nodes
        - As well as the Kubernetes 
- We can also use logging and monitoring
    - Could be common for front and backback 
    - We have a logging for baremetal AND K8 platform
- We can use networking and security tools
    - Imagine in Backend we have private data, only accessible via private end-points
    - In frontend, imagine we don't really care and want to access via public end-points
        - Public doesn't mean not secure 
    - Now, how does the front-end communicate with the backend ?!
        - We use another cloud tool, such as a VPN Gateway
        
That's some features and capabilities that are available on a public cloud

### Hybrid Cloud
Imagine a freight company that has an existing private server. On it, there's a BFF, an ERP and a User Data part. Now, they want to create a new mobile application, which will of course need a new BFF.
- They decided to create this new BFF
