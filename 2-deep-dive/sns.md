# SNS - Simple Notification Service

- Why is SNS needed? For example, can't we just create some logic in our Order Service to publish messages to all the other services (Inventory, Notification, and Shipping).
    - Answer: you need to make the logic yourself which is hard to mannage. You will have to write code for the following:
        - **Decoupling**: The Order Service would have to maintain knowledge of all subscriber services, including their APIs and how to interact with them. This leads to tighter coupling. Changes to any subscriber (like adding a new one or modifying an existing one) would require updates to the Order Service’s codebase, making it less maintainable.
        - **Scalability**: The Order Service would need to implement logic to manage the load itself **??**, potentially having to queue messages within its code or using a local load balancer to distribute requests **??**. Scaling each subscriber would also require direct modifications to the Order Service, which complicates the architecture and can introduce single points of failure.
        - **Flexibility**: The Order Service would need to implement conditional logic to determine how to send notifications based on the current method of communication (e.g., moving from email to mobile notifications). This would increase complexity and potentially introduce bugs if different notification paths are not properly maintained.
        - Reliability: The Order Service would need to implement its own retry logic to handle failures when communicating with other services. This could involve complex error handling and state management to ensure messages are eventually processed, leading to a less robust system.
        - **Asynchronous Processing**: The Order Service would need to wait for each subscriber to complete its processing before sending a response to the user.
        - **Load Distribution**: Each subscriber would need to implement its own load balancing **??**, potentially requiring additional infrastructure. The Order Service would have to include logic to manage concurrent requests and ensure that notifications are processed efficiently, complicating the system architecture.
        - **Integration with Other Services**: The Order Service would need to handle the integration logic, which includes retries, error handling, and maintaining the state of communications with multiple services. This tight integration would reduce the overall flexibility of the system and make it harder to implement new features or change existing ones.
- Pub/Sub model
- The event produces only sends messages to one SNS topic
- Each subscriber to the topic will get all the messages be default (we can filter them, if we want)
- We can have up to 10 million subscribers per topic
- We cave up to 100K topics
- Subscribers to the topic can be:
    - SQS
    - HTTP/HTTPS
    - Lambda
    - Emails
    - SMS messages
    - Mobile Notifications
- Many different services integrate with SNS for notifications, for example:
    - CloudWatch (for alarms)
    - Auto Scaling Groups notifications
    - S3 (bucket events)
    - CloudFormation (state changes)
    - Etc...
- How to publish?
    - In order to publish we must create a topic using the SDK
    - We may create one or many subscriptions
    - We publish data to the topic
- Direct Publish (for mobile apps SDK)
    - Create a platform application
    - Create a platform endpoint
    - Publish to the platform endpoint
- Direct Publish works with Google GCM, Apple APNS, Amazon ADM

## Security

- Encryption:
    - In-flight encryption using HTTPS API
    - At-rest encryption using the KMS keys
    - Client-side encryption if the client wants to perform encryption/decryption itself
- Access Controls: IAM policies to regulate access to the SNS API
- SNS Access Policies (similar to S3 bucket policies):
    - Useful for cross-account access to SNS topics
    - Useful for allowing other services (S3) to write to an SNS topic

## SNS + SQS Fan Out
- Why use SQS ontop of SNS??
- SNS vs SQS vs Eventbridge: https://www.youtube.com/watch?v=RoKAEzdcr7k&ab_channel=BeABetterDev
- Send a message to multiple SQS queues using SNS
- Push one in SNS, receive in all SQS queues which are subscribers
- Fully decouples, no data loss
- SQS allows for data persistance, delayed processing and retries of work
- Ability to add more SQS subscribers over time
- SQS queues must have an allow access policy for SNS to be able to write to the queues
- **SNS cannot send messages to SQS FIFO queues (AWS limitation)!**
- Use case: send S3 events to multiple queues:
    - For the same combination of even type and prefix we can only have one S3 Event rule
    - In case we want to send the same S3 event to many SQS queues, we must use SNS fan-out
