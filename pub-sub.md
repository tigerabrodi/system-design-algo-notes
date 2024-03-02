# Publish/Subscribe Pattern

Imagine you've this problem: you have a system where you have a lot of users, and you want to send them notifications. You could send them notifications directly, but this would be inefficient. Instead, you could use the publish/subscribe pattern.

The pub sub pattern consists of 4 main components:

- Publisher: This is the component that sends messages. In our example, this would be the component that sends notifications to users.
- Subscriber: This is the component that receives messages. In our example, this would be the component that receives notifications from the publisher.
- Topic: This is the channel that the publisher sends messages to. In our example, this would be the channel that the publisher sends notifications to.
- Message: This is the data that the publisher sends to the subscriber. In our example, this would be the notification that the publisher sends to the subscriber.

The pub sub pattern is useful because it allows you to decouple the publisher from the subscriber. This means that the publisher doesn't need to know who the subscriber is, and the subscriber doesn't need to know who the publisher is. This is useful because it allows you to add new publishers and subscribers without changing the existing publishers and subscribers.

The publishers publish message to a specific topic. Each topic can be seen as a channel of specific type of messages, for example, a topic could be "notifications", and the messages could be "new video uploaded", "new comment", etc.

Subscribers can subscribe to a specific topic, and they will receive all messages published to that topic. For example, a user could subscribe to the "notifications" topic, and they would receive all notifications published to that topic.

## Message Delivery Guarantees

We have different types of delivery guarantees:

- At most once: The message is delivered at most once, or it may not be delivered at all.
- At least once: The message is always delivered, but it may be delivered more than once.
- Exactly once: The message is always delivered exactly once.

Let's say a subscriber is offline, and a message is published to a topic. When the subscriber comes back online, it will receive the message. This is an example of at least once delivery.

Let's say a message is published to a topic, and the subscriber receives the message. The subscriber then sends an acknowledgment to the publisher. If the publisher doesn't receive the acknowledgment, it will send the message again. This is an example of at most once delivery.

Let's say a message is published to a topic, and the subscriber receives the message. The subscriber then sends an acknowledgment to the publisher. If the publisher doesn't receive the acknowledgment, it will send the message again. The subscriber will then check if it has already processed the message, and if it has, it will ignore the message. This is an example of exactly once delivery.

## Idempotent

When a message is delivered more than once, it's important that the message is idempotent. This means that the message can be processed multiple times without changing the result. This is important because it ensures that the message can be processed multiple times without causing any problems. For example, if a message is delivered more than once, and the message is idempotent, then the message can be processed multiple times without causing any problems.

## Ordering

When messages are published to a topic, they are delivered to the subscribers in the order they were published. This is important because it ensures that the messages are delivered in the correct order. For example, if a message is published before another message, then it should be delivered before the other message.

Some pub/sub solutions out there will give you the ability to replay/rewind messages, so if you have a new subscriber, it can go back and read all the messages that were published to a topic before it subscribed.

## Why multiple topics?

You might be wondering why we need multiple topics. The reason is that it allows you to have different types of messages. For example, you might have a "notifications" topic for notifications, and a "comments" topic for comments. This is useful because it allows you to have different types of messages, and different subscribers for those messages.

## Popular tools

Some popular pub/sub tools are:

- Google Cloud Pub/Sub
- Amazon SQS
- RabbitMQ
- Redis
- Kafka

Some of them offer nice solutions e.g. replayability or Google Cloud Pub/Sub offers scalability out of the box, you don't need to worry about scaling topics or redundancy of topics.
