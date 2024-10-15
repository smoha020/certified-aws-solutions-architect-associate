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
