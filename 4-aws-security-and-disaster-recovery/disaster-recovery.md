# Disaster Recovery

- Disaster: any event that has a negative impact on a company's business continuity or finances
- Disaster Recovery (DR) is about preparing for and recovering from a disaster
- Disaster recovery solutions:
    - On-premise to on-premise: traditional DR, expensive
    - On-premise to cloud: hybrid recovery
    - AWS Cloud Region A to AWS Cloud Region B

## RPO and RTO

- RPO - Recovery Point Objective: How often we create backups. Time between the RPO and the disaster is the data loss
- RTO - Recovery Time Objective: The point in time when the recovery finishes. The time between the disaster and the RTO is downtime

## Disaster Recovery Strategies

- Backup and Restore: high RPO, cheap, easy to manage and accomplish
- Pilot Light:
    - A small version of the app is always running in the cloud (example: EC2 not running but RDS is running)
    - Useful for critical core (pilot light)
    - Similar to backup and restore strategy
    - Faster than backup and restore as critical system are already running
- Warm Standby
    - Full system is up and running but at a minimal size (example: Autoscaling group redirects traffic from on prem DB to RDS???) 
    - Upon disaster we can scale to production load
- Hot Site / Multi Site Approach
    - Very low RTO - very expensive
    - Full production scale is running on the cloud
- All AWS Multi Region

## Disaster Recovery Tips

- Backups:
    - EBS Snapshots, RDS, automated backups, snapshots, etc.
    - Regular pushes to S3/S3 IA/Glacier, Lifecycle Policy, Cross region replication
    - From on-premise: Snowball or Storage Gateway
- High Availability:
    - Use Route53 to migrate DNS over from region to region (**Migrate DNS???**)
    - RDS Multi-AZ, ElastiCache Multi-AZ, EFS, S3
    - Site to site VPN as recovery from Direct Connect
- Replication:
    - RDS Replication (Cross Region), AWS Aurora + Global Databases
    - Database replication from on-premise to RDS
    - Storage Gateway
- Automation:
    - CloudFormation/Elastic Beanstalk to recreate a whole new environment
    - Recover/Reboot EC2 instances with CloudWatch if alarm is in fail state (ALARM)
    - AWS Lambda for customized automation
- Chaos
    - Netflix has a "simian-army" randomly terminating EC2 instances

## On-Premise Strategy with AWS

- Ability to download Amazon Linux 2 AMI as a VIM (iso format)
- VM Import/Export:
    - Ability to migrate existing applications into EC2
    - Ability to create a DR repository for on-premise VMs
    - Ability to export back the VMs form EC2 to on-premise
- AWS migration big picture
    - https://aws.amazon.com/blogs/architecture/accelerating-your-migration-to-aws/
    - <img width="413" alt="image" src="https://github.com/user-attachments/assets/fd633108-fe20-43db-9f09-035003bd65c7" />

- AWS Application Discovery Service:
    - This service is BEFORE you do the migration (with MGN)
    - Agentless vs Agent-based discovery
        - <img width="533" alt="image" src="https://github.com/user-attachments/assets/40910045-3d5e-4933-8d51-dbdeda518675" />
    - Gather information about on-premise servers to plan a migration
    - Provides information about server utilization and dependency mappings
    - Track all migrations with AWS Migration Hub
        - https://aws.amazon.com/blogs/mt/using-aws-migration-hub-network-visualization-to-overcome-application-and-server-dependency-challenges/
        - <img width="448" alt="image" src="https://github.com/user-attachments/assets/e8d7de33-6e10-4844-83c1-c5bd15571ec0" />

- AWS Database Migration Service (DMS)
- AWS Application Migration Service (MGN)
    - Migrate applications such as SAP, Oracle, and SQL Server running on physical servers, VMware vSphere, Microsoft Hyper-V, and other on-premises infrastructure.
    - <img width="535" alt="image" src="https://github.com/user-attachments/assets/8fc0e0c4-e570-4425-9eb4-f52553b3728e" />
- AWS Server Migration Service (SMS): **??**
    - Incremental replication of on-premise live servers to AWS

## RDS & Aurora MySQL Migration
- Scenrario: You want to migrate data from RDS MySQL to Aurora MySQL. Here are the options:
    - <img width="456" alt="image" src="https://github.com/user-attachments/assets/49aa1238-0362-4645-b22b-f9ba687c851e" />
    - Option: RDS to Aurora using Read Replica:
        - https://aws.amazon.com/getting-started/hands-on/migrate-rdsmysql-to-auroramysql/
    - On Prem MySQL to Aurora using Percona:
        - https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/migrate-on-premises-mysql-databases-to-aurora-mysql-using-percona-xtrabackup-amazon-efs-and-amazon-s3.html
        - ![image](https://github.com/user-attachments/assets/2dfce81c-d48d-4cec-b285-53c6f9e76509)
