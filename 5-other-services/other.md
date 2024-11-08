# Other Services

## SES
- Send emails

## Pinpoint
- Send email, SMS, push, voice, and in-app messaging.
- You can receive replies
- **Use Case**: run campaigns by sending marketing, bulk, transactional SMS messages
- Example of apps with push notification: WhatsApp. It sends push notifications to alert users when they receive new messages, even when the app is not open. Other examples include social media apps like Facebook or Instagram, which notify users about likes, comments, or new messages
- **Pinpoint vs SES vs SNS**:
    - Pinpoint allows for text and push notifications.
    - With Pinpoint it's easier to set up tempates, manage the different people your sending to. You don't need to this programatically from inside an app you built.

## AWS SSM Manager
- Allows you to do SSH to your EC2
- **SSM Manager vs Instance Connect**:
    - Instance connect needs you to open SSH port
    - SSM Manager is only for SSH-ing to Amazon Linux machines
    - You need to attach a role to the EC2 in order to use SSM Manager
- SSM Manager services
    - Run Command, Patch Manager, Maintenance Window,
    - Automation: automate tasks such as restarting EC2, creating EBS snapshots

 
## AWS Cost Explorer
- We can create a savings plan

## AWS Cost Anomally Detection
- Monitors your cost and usage with the help of ML and then sends you a report.
- You can notified periodically

## Batch
- **Batch vs Lambda**: ???
<details>
<summary>Batch Job Examples</summary>
<br>
In the context of software development, **batch jobs** refer to processes or tasks that are executed without user interaction, typically on a scheduled basis, and handle large volumes of data or repetitive operations. These jobs are often designed to run in the background during off-peak hours to optimize system performance and avoid overloading resources. Below are some common examples of **batch jobs** in software development:

### 1. **Data Backup and Archiving**
   - **Description:** Periodic backups of databases or file systems to ensure data integrity and disaster recovery.
   - **Example:** A batch job that backs up the entire database every night at midnight, creating snapshots of critical data files or moving old data into an archive.

### 2. **Data ETL (Extract, Transform, Load)**
   - **Description:** Jobs that collect data from various sources, transform it into a desired format, and load it into a data warehouse or other systems.
   - **Example:** A batch job runs every night to extract sales transaction data from different sources (e.g., an e-commerce platform, CRM system), transforms it (e.g., aggregating totals, converting currency), and loads it into a data warehouse for reporting.

### 3. **Log File Rotation and Cleanup**
   - **Description:** Jobs that manage and clean up log files that may accumulate over time.
   - **Example:** A batch job that rotates server log files every day, compresses older logs, and deletes logs that are older than a certain period (e.g., 30 days).

### 4. **Email Campaigns (Mass Email Sending)**
   - **Description:** Sending bulk emails to customers, users, or subscribers, often for marketing, notifications, or reminders.
   - **Example:** A batch job runs every morning to send out a marketing email to all users who opted into a weekly newsletter or promotional campaign.

### 5. **Report Generation**
   - **Description:** Automating the generation of periodic reports, such as financial, inventory, or user activity reports.
   - **Example:** A batch job that generates end-of-day financial reports every night, summarizing daily transactions and balances for accounting purposes.

### 6. **Data Cleansing and Validation**
   - **Description:** Jobs that clean, validate, and standardize data before it's used in other processes, such as analytics or reporting.
   - **Example:** A batch job runs overnight to check user records for incomplete or invalid data (e.g., missing addresses, incorrect phone numbers) and either corrects or flags the problematic entries.

### 7. **System Health Checks and Maintenance**
   - **Description:** Jobs that ensure the system’s resources (disk space, database health, etc.) are operating correctly and that any necessary maintenance tasks are completed.
   - **Example:** A batch job that runs weekly to check the health of the database, rebuilds indexes, checks for disk space issues, and clears temporary system files.

### 8. **Data Synchronization Between Systems**
   - **Description:** Periodic synchronization between systems, ensuring that data in different databases or applications stays consistent.
   - **Example:** A batch job runs every hour to synchronize data between an e-commerce platform's inventory system and the accounting system, ensuring stock levels are updated in both places.

### 9. **Image/Video Processing**
   - **Description:** Batch jobs that process large numbers of files (e.g., images or videos) in bulk, such as resizing, compressing, or converting file formats.
   - **Example:** A batch job that processes and compresses images uploaded by users on an image-sharing platform, converting them to a consistent size and format for optimized web display.

### 10. **Credit Card Payment Reconciliation**
   - **Description:** Matching and reconciling payment transactions with bank statements or credit card processors.
   - **Example:** A batch job that runs at the end of each month to reconcile customer payments made through credit cards with the payment gateway's transaction logs and bank statements.

### 11. **File and Data Import/Export**
   - **Description:** Periodic imports or exports of large datasets, often from or to external systems, such as customer data, product catalogs, or transaction logs.
   - **Example:** A batch job that runs daily to export customer order data from an internal system to a third-party fulfillment provider's system in a CSV file.

### 12. **Sending SMS Notifications**
   - **Description:** Automated sending of SMS alerts or reminders in bulk, such as appointment reminders or system alerts.
   - **Example:** A batch job that sends reminders to customers about upcoming appointments or subscription renewals via SMS at scheduled intervals.

### 13. **Data Migration**
   - **Description:** Moving data from one system or database to another, often as part of an upgrade or migration project.
   - **Example:** A batch job that performs nightly data migrations from a legacy system to a new cloud-based system, ensuring that all the data is transferred and synchronized.

### 14. **Sending Daily/Weekly Summaries**
   - **Description:** Jobs that send periodic summaries to users or administrators based on system activity or performance metrics.
   - **Example:** A batch job that sends weekly performance reports to system administrators summarizing server health, error logs, and usage metrics.

### 15. **Batch Data Analysis**
   - **Description:** Analyzing large datasets and generating aggregate insights or predictions in bulk, often running periodically to support business decisions.
   - **Example:** A batch job that analyzes user activity logs and generates weekly insights on user behavior, which is then used to optimize marketing campaigns.

### 16. **Order Processing (in E-commerce)**
   - **Description:** Automatically processing orders, including inventory updates, order status changes, and customer notifications.
   - **Example:** A batch job that processes all new orders placed after business hours, updating stock levels, calculating taxes and shipping costs, and notifying customers of their order status.

### 17. **Data Anonymization or Masking**
   - **Description:** Jobs that anonymize or mask sensitive data, ensuring compliance with privacy regulations like GDPR or CCPA.
   - **Example:** A batch job that runs at regular intervals to anonymize customer data in logs, such as replacing email addresses with random identifiers, to ensure that the system complies with data privacy laws.

### 18. **Data Aggregation for Machine Learning Training**
   - **Description:** Collecting and aggregating datasets to prepare them for training machine learning models.
   - **Example:** A batch job that aggregates historical transaction data, user behavior data, and product details to create a dataset for training a recommendation system.

### 19. **Automatic Software Update Checks**
   - **Description:** Jobs that check for updates to libraries, frameworks, or dependencies, and download or notify the system about new versions.
   - **Example:** A batch job that runs weekly to check for and download security patches for the software stack, such as updating the operating system, libraries, or server software.

### 20. **Archiving Old Records**
   - **Description:** Archiving or purging old records that are no longer actively used but may still be required for compliance or auditing purposes.
   - **Example:** A batch job that runs monthly to move transaction logs older than 2 years from an active database to long-term archival storage for compliance purposes.

---

**Key Characteristics of Batch Jobs**:
- **Non-Interactive:** They run automatically without user intervention.
- **Scheduled:** Batch jobs are typically scheduled to run at regular intervals (e.g., hourly, daily, weekly).
- **Efficient for Large Datasets:** They are designed to process large volumes of data in one go.
- **Resource-Intensive:** Batch jobs can consume a lot of system resources, so they often run during off-peak hours to minimize impact on other operations.

Batch jobs are a fundamental aspect of many enterprise systems, especially those that need to handle large-scale data processing, reporting, and automation efficiently.
</details>

## AppFlow
- Transfer data from SaaS applications like Salesforce, SAP, Zendesk, Slack, and ServiceNow to AWS or other destinations
- **Use Case**: transfer the data in the accounts table from Sales Force to an S3 bucket as an excel file https://www.youtube.com/watch?v=RfFXxVt3l0k&ab_channel=NamrataHShah

## Amplify
- Remove complexiity for developers using Amplify commands.
- **Use Case**: You want to create some apis and deploy them quickly. Once you write your code, you then run some amplify commands to deploy your code. Behind the scenes Amplify will use terraform to spin up an API gateway and a Lamda function. https://www.youtube.com/watch?v=HkbjHtG_d7w&ab_channel=BeABetterDev



## AWS Opsworks

- Chef and Puppet are open source platforms and allow to perform server configuration automatically
- They work great with EC2 and on-premise VM
- AWS Opsworks = Managed Chef and Puppet
- Alternative to AWS SSM

### Chef and Puppet

- They help with managing configuration as code which helps in having consistent deployments
- Work on Linux/Windows
- We can automate: user accounts, cron jobs, ntp, packages, services, etc.

## Elastic Transcoder

- Convert media files (video + music) stored in S3 into various formats for tables, PCs, smartphones, TVs, etc.
- Features:
    - Optimize bite rate
    - Create thumbnails
    - Create watermarks
    - Create captions
    - DRM
    - Provides progressive download
    - Encryption
- 4 components of Elastic Transcoder:
    - Jobs: what does the work of the transcoder
    - Pipeline: queue that manages the transcoding job
    - Presets: templates for converting media from one format to another
    - Notifications
- Pay for what we use, scales automatically, fully managed
