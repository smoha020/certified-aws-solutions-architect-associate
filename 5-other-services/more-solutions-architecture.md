# More Solution Architecture

## Event Processing

- SQS + Lambda:
    - Lambda functions pulls the SQS queue, in case there is a problem, the message is put back onto the queue for reprocessing
    - To avoid endless loops in processing, we can set up a deal-letter queue (DLQ)
- SQS FIFO + Lambda:
    - If a message is not processed, it can block the whole queue
    - In order to get around this, we can also set up a DLQ
- SNS + Lambda:
    - In case a message is not processed, the Lambda will retry 3 times
    - We can also set up a DLQ at the Lambda service level
- Fan Out Pattern:
    - Deliver messages to multiple SQS queues
    - In order to achieve this, we can create an SNS topic and create SQS queue subscribers
    - We can combine Fan Out pattern with S3 events
    - We can also create filter to filter out some events and react to only what is needed
    - We can create as many S3 events as we want 
    - If two events are happening on the same object on the same time, there is a possibility that only one event notification is sent. To overcome this we can use versioning

## Caching Strategies

- CloudFront: caching happens globally as close as possible to the users
- API Gateway: offers regional caching
- Redis, Memcached, DAX: caching is closer to the application. The reason for this is to avoid load on a database

## Blocking an IP Address in AWS

- Network ACL, VPC level: create a deny rule
- Security Groups: define a subset of IP which can access the application
- Optional firewall installed on the instance
- In case of an Application Load Balancer:
    - ALB does connection termination, from the EC2 side we just have to approve traffic from the ALB
    - In the SG of the LB we can specify from where the traffic can came from
    - We can also install WAF on the ALB, where we can do some complex filtering
- In case of Network Load Balancer:
    - NLB does not do connection termination, there is no such thing as a SG for the NLB
- In case of CloudFront:
    - CloudFront seats outside of a VPC, so we can not set NACL rules
    - In this case to block a client on CloudFront, we can do the following:
        - Use georestriction to restrict the country from where traffic is coming from
        - Use WAF IP Address filtering on the CloudFront distribution

## High Performance Computing (HPC)
<details>
<summary>What is it?</summary>
<br>
**High Performance Computing (HPC)** refers to the use of powerful computer systems to perform complex calculations and process large datasets at high speeds. It involves utilizing parallel processing and specialized hardware architectures to solve problems that would be infeasible for standard desktop or server computers due to computational, memory, or I/O constraints. HPC is commonly used in scientific research, engineering, simulations, data analysis, and any domain requiring intensive computation.

### Key Aspects of High Performance Computing

1. **Parallel Computing**
   - **Parallelism** is at the heart of HPC. Rather than performing calculations sequentially, HPC systems use multiple processors (CPUs or GPUs) working together in parallel to break down a problem into smaller tasks and execute them simultaneously.
   - This is made possible through **parallel algorithms** that decompose a problem into smaller sub-problems that can be solved concurrently.
   - **Shared memory systems** or **distributed memory systems** can be used, where memory is either shared among all processors or spread across multiple nodes, respectively.

2. **Supercomputers and Clusters**
   - HPC is typically realized using **supercomputers** or **HPC clusters**.
     - **Supercomputers** are highly specialized machines with massive computational power, such as the Cray systems or IBM Blue Gene.
     - **HPC clusters** are groups of interconnected computers (nodes) that work together as a single system to perform parallel processing. These nodes can be commodity hardware or specialized systems, all linked by high-speed networks to communicate efficiently.

3. **Specialized Hardware**
   - **CPUs** (Central Processing Units): General-purpose processors, often used in traditional HPC systems, where multiple cores are utilized for parallel tasks.
   - **GPUs** (Graphics Processing Units): GPUs are specialized for parallel processing and are highly effective in handling workloads like machine learning, deep learning, and scientific simulations. GPUs have thousands of smaller cores that can handle highly parallel tasks simultaneously.
   - **FPGAs** (Field-Programmable Gate Arrays) and **ASICs** (Application-Specific Integrated Circuits): These are specialized hardware solutions for specific high-performance tasks. They offer significant performance improvements for tasks like cryptography, signal processing, and custom algorithm processing.
   
4. **High-Speed Interconnects**
   - In HPC, communication speed between processors or nodes is crucial. High-speed interconnects, like **InfiniBand**, **Fibre Channel**, or **Ethernet**, are used to ensure that data can be transferred quickly across nodes to avoid bottlenecks.
   - **Low latency** and **high bandwidth** are critical to ensure that parallel tasks can communicate efficiently and scale well as the number of nodes increases.

5. **Storage Systems**
   - **Parallel File Systems**: HPC often involves dealing with massive datasets, so fast, distributed storage solutions are essential. Parallel file systems, such as **Lustre** or **GPFS** (General Parallel File System), provide high throughput and low latency for handling large volumes of data.
   - **Storage Hierarchies**: HPC systems typically feature multi-layer storage architectures, from high-speed solid-state drives (SSDs) for fast access to memory-resident data, to large-scale disk arrays for bulk storage of less frequently accessed data.

6. **Scalability**
   - HPC systems are designed to **scale** to accommodate increasing computational needs. Scalability is achieved by adding more processors, nodes, or memory to the system to improve performance. HPC workloads are often highly **scalable**, meaning that they can efficiently utilize more resources as they become available, making them suitable for very large tasks like simulations of physical systems, climate modeling, or big data analytics.

7. **Job Scheduling and Resource Management**
   - **Schedulers** like **Slurm**, **PBS** (Portable Batch System), or **Torque** are used in HPC environments to manage the allocation of resources (CPU, memory, storage) and to schedule and queue jobs.
   - These tools ensure that users and programs are allocated the necessary resources based on priority, job requirements, and availability, ensuring efficient use of the system.

### Applications of HPC

HPC is employed in a variety of fields where performance and computation power are critical:

1. **Scientific Research and Simulations**
   - **Climate Modeling**: Simulating climate systems, weather patterns, and predicting global warming scenarios.
   - **Physics**: Simulating particle collisions (e.g., at CERN), astrophysics simulations, and material science.
   - **Genomics**: Processing massive amounts of DNA sequencing data for research in biology and medicine.

2. **Engineering and Design**
   - **Finite Element Analysis (FEA)**: Used in mechanical engineering to simulate physical stresses and forces on structures or products, such as airplanes or automotive parts.
   - **Computational Fluid Dynamics (CFD)**: Simulating fluid flow for design optimization in areas like aerospace, automotive, and civil engineering.

3. **Artificial Intelligence (AI) and Machine Learning (ML)**
   - HPC accelerates the training of deep learning models, especially for large datasets, using **GPU** or **TPU** (Tensor Processing Unit)-based systems.
   - HPC infrastructure is required for tasks like **natural language processing** (e.g., training large language models like GPT), **image recognition**, and **autonomous vehicle systems**.

4. **Big Data Analytics**
   - HPC is essential for processing and analyzing massive datasets in real-time or batch modes, such as in **financial modeling**, **social media sentiment analysis**, or **genomic research**.
   - Tools like **Hadoop**, **Spark**, or **Apache Flink** are often deployed in an HPC environment to process data in parallel across a distributed computing network.

5. **Medical Imaging and Healthcare**
   - **Medical Image Processing**: HPC is used to process complex medical imaging data, such as MRIs, CT scans, or genetic data, to provide faster diagnosis and personalized treatment recommendations.
   - **Drug Discovery**: Simulations of molecular interactions or protein folding to accelerate the development of new drugs.

6. **Government and Defense**
   - HPC is used in **cryptography**, **intelligence gathering**, and **military simulations** (e.g., battle simulations, defense system design).
   - **National Security**: Analyzing large datasets to detect cyber threats or simulate security scenarios.

### Challenges in HPC

While HPC is powerful, it also presents several challenges:

1. **Cost**
   - High-performance hardware and infrastructure (supercomputers, specialized hardware like GPUs, and storage systems) can be extremely expensive to build and maintain.
   
2. **Power Consumption**
   - HPC systems consume significant amounts of electricity, particularly as they scale up in size, which can lead to substantial operating costs. Optimizing power consumption is a growing focus in HPC research.

3. **Software and Algorithm Efficiency**
   - Developing software that efficiently utilizes parallel computing resources is challenging. Writing parallel algorithms requires special programming techniques, such as **MPI** (Message Passing Interface), **OpenMP**, or **CUDA** for GPU programming.
   
4. **Data Management**
   - The sheer volume of data generated and processed by HPC systems requires advanced data management techniques, especially in terms of storage, retrieval, and real-time processing.

5. **Cooling and Physical Space**
   - Due to their massive computational power, HPC systems generate significant amounts of heat. Effective cooling solutions (e.g., liquid cooling, cryogenic cooling) and physical infrastructure to house these systems are essential.

### Examples of HPC Systems

1. **Supercomputers:**
   - **Fugaku** (Japan): Currently one of the world’s fastest supercomputers, developed by RIKEN and Fujitsu. It has been used for research in drug development, climate modeling, and disaster prediction.
   - **Summit** (USA): Developed by IBM and installed at Oak Ridge National Laboratory, used for scientific research in areas like genomics and materials science.
   
2. **Cloud-based HPC:**
   - Many organizations use cloud providers such as **Amazon Web Services (AWS)**, **Microsoft Azure**, and **Google Cloud** to run HPC workloads. These platforms provide scalable, on-demand access to powerful compute resources, enabling users to run simulations, large-scale analyses, and machine learning models without maintaining physical hardware.

---

### Conclusion

**High Performance Computing (HPC)** enables the processing of complex problems that require vast amounts of computational power, data storage, and fast interconnects. By utilizing parallel computing techniques and specialized hardware, HPC accelerates research and innovation across many scientific, engineering, and business domains. As computational needs continue to grow, HPC plays an increasingly crucial role in solving some of the world’s most pressing challenges, from climate change to AI-driven medical advancements.
</details>

- The cloud is the perfect place to perform HPC
- We can use HPC to perform genomics, computational chemistry, financial risk modeling, weather prediction, machine learning, deep learning, etc.
- Data Management and Transfer:
    - AWS Direct Connect: move GB of data to the cloud over private secure network
    - Snowball and Snowmobile: move PB of data to the cloud
    - AWS DataSync: move large amount of data between on-premise and S3, EFS, FSx
- Compute and Networking:
    - EC2 Instances:
        - CPU optimized and GPU optimized
        - Spot instances/spot fleets for cost saving + auto scaling
    - EC2 Placement Groups:
        - Cluster placement group for good network performance
    - EC2 Enhanced Networking (SR-IOV):
        - Higher bandwidth, higher packet per second, lower latency
        - How to get Enhanced Networking:
            - Option 1: Elastic Network Adapter (ENA) up to 100 Gbps
            - Option 2: Intel 82599 VF up to 10 GBps - Legacy
    - Elastic Fabric Adapter (EFA)
        - Improved ENA for HPC, only works for Linux
        - Great for inter-node communications, tightly coupled workflows
        - Leverages Message Passing Interface (MPI) standards
        - Bypasses the underlying Linux OS to provide low-latency, reliable transport
- Storage:
    - Instance-attached storage:
        - EBS: scales up to 64000 IOPS with io1 Provisioned IOPS
        - Instance Store: scales to millions of IOPS, linked to EC2 instance, low latency
    - Network storage:
        - S3: for large blobs
        - EFS: scale IOPS based on total size or we can use provisioned IOPS
        - FSx for Lustre: HPC optimized distributed file system, provides millions of IOPS, backed by S3
- Automation and orchestration:
    - AWS Batch:
        - Supports multi-node parallel jobs, which enables to run single jobs that can span across multiple EC2 instances
        - We can easily schedule jobs and launch EC2 instances accordingly
    - AWS ParallelCluster:
        - Open source cluster management tools to deploy HPC on AWS
        - It is configured with text files
        - Automate creation of VPC, Subnet, cluster type and instance types


## Highly Available EC2 Instances

1. Option:
    - Main EC2 instance with Elastic IP + standby EC2 instance for failover
    - EC2 instance can be monitored with CloudWatch Events + Lambda functions. Using this method we can failover in case of an issue.
2. Option:
    - ASG in 2 availability zones
    - ASG settings: 1 min, 1 max, 1 desired
    - In case of failover the new instance will be launched in the second AZ
    - The Elastic IP can be attached to the instance with using an user data script
3. Option:
    - Setup is same as option 2 + EBS
    - ASG can use lifecycle groups, based on these we can create an EBS snapshot and attach it to the newer instance

## Highly Available Bastion Hosts

- Bastion hosts can be created in multiple subnet, same VPC
- We can create a Network Load Balancer which can route traffic to multiple bastion hosts
