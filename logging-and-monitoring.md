# Logging and Monitoring

What is logging and monitoring?

Imagine you're running a website like Youtube, and you have millions of users. You want to know how many users are using your website, how many videos are being watched, and how many users are uploading videos. You also want to know how many users are getting errors, and what those errors are. This is where logging and monitoring come in.

Let's say for Youtube Premium, someone may subscribe, and it may tell them success, but they can't access the premium content, they reach out to your support team, and they can't figure out what's wrong. You need to know what's happening in your system, and this is where logging and monitoring come in.

## Logging

Let's imagine this is happening locally and you're debugging, you would then as a developer print out the error message to the console. But when you're running a distributed system, you can't just print out to the console, you need to log it to a file, or a database, or a log management system. This is because the system is deployed and the error is happening on a server, and you can't just go to the server and look at the console.

Logging is the process of recording events that happen in your system. These events can be anything from a user logging in, to a server error. Logging is important because it allows you to see what's happening in your system. This is important because you need to know what's happening in your system. You might need to know how many users are getting errors. This is why logging is important.

When adding logs to your system that will be visible in e.g. a log management system, can be provided by a logging library. This library will allow you to log messages at different levels, such as `info`, `warning`, `error`, etc. This is important because you might want to log different messages at different levels. For example, you might want to log an error message at the `error` level, and a warning message at the `warning` level.

The format of logs will typically be syslog or JSON. This is because these formats are easy to read and write.

## Monitoring

Monitoring is similar to logging, its a tool or system that watches your system. It watches your system to see if it's working as expected.

This includes things like:

- Health checks
- Uptime checks
- Error rate
- Latency
- Traffic

You can imagine if you're building a system like Youtube, you may want to know the latency of your system, how long it takes for a user to upload a video, how long it takes for a user to start watching a video, etc.

You will wanna configure alerts, so if error rate goes above a certain threshold, you will get an alert. This way you can quickly respond to issues in your system.

You can also hook up your monitoring system in a place where you can see it and get the alerts e.g. if you're using Slack, you can hook it up to Slack.

## Time series databases

To gather metrics, you will often use a time series database. This is because time series databases are optimized for time series data. This is important because you will often need to store time series data. For example, you might need to store the number of users that are using your system at a given time. This is why time series databases are important.
