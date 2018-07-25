# Amazon SQS - Simple Queue Service
- Buffer between components writing messages and components reading and processing messages
- 256 kb message
- for > 256KB, use SQS Extended client, which stores payloads in S3.
- Has at least once delivery in normal state
- FIFO queues are supported
    - no duplicates
    - ordering is guaranteed
- SQS is region specific (not cross region)
- Messages can be retained for 14 days
- Long polling reduces extraneous polling
- SQS priority is not supported
    - Use two queues. Processing server should check high-priority queue first.
- Architecture
    - Fanout architecture
        - Msg sent to SNS topic, then spread accross several SQS queues, each related to a spicific processing need
            - For example, image arrived, sent to SQS queues: Thumbnail Generation, Image Recognition, Scan Metadata.
    - Order processing:
        - Webservers send order to SQS, don't wait for answer.