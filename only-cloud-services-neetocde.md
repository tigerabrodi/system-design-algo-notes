# The only cloud services you actually need to know

## VM

You can think of a VM as renting a computer in the cloud. You can install whatever you want on it, and it's yours to use as you please. You can use it to run a web server, a database, or anything else you can think of.

While you might not actually rent a computer, that's the perspective when working with VMs.

VM stands for "Virtual Machine".

Every other cloud service is built on top of VMs. They're the foundation of cloud computing.

This is an example of an unmanaged service. The only thing the cloud providers does for you is provisioning the resource to use, but not managing it for you.

You will likely connect to the VM e.g. via SSH.

Examples: AWS EC2, Google Compute Engine, Azure Virtual Machines.

## Object stores

What if you want to store files?

That's where object stores come in. Your only concern is reading and writing files, you don't need to worry about the underlying infrastructure. As compared to VMs where you have to specify the size of the VM, the amount of memory, the number of CPUs, etc.

With an object store, you just upload and download files. The cloud provider takes care of the rest.

You're still under the hood gonna need memory, CPU, etc. but don't worry about it. This is an example of a managed service. The cloud provider takes care of the infrastructure for you, and you just use it.

This is also sometimes called serverless, because you don't need to worry about servers. Under the hood, files are replicated across multiple servers, so you don't need to worry about losing your data as compared if you had a sinlge point of failure.

Examples: AWS S3, Google Cloud Storage, Azure Blob Storage.

## Database services

What if you had actual application data?

Databases are complex. You will wanna run something like MySQL, PostgreSQL, or MongoDB. Databases are just a really complex wrapper around particularly disk space. You could run a database on a VM, specify the size etc, replicate it across multiple VMs, sharding, but that's a lot of manual and complex work.

That's why cloud providers offer you a managed database service.

In the world of AWS, relational database would be RDS, and non-relational database would be DynamoDB.

### Proprietary services

In many cases, AWS isn't doing anything creative, they're just taking open source software and running it for you. But in some cases, they have proprietary services.

For example, DynamoDB is a proprietary service. It's not open source, and it's not something you could run on your own. If you decided to migrate from DynamoDB to a different non relational database because it's e.g. too expensive, you would have to migrate your data, and you would have to change your application code.

This is also referred to as vendor lock-in. Generally, you don't want to be locked into a single vendor. However, in some cases, the proprietary service is so good that it's worth the trade-off.

## Knowing one cloud sets you off

Every cloud provider offer similar services.

Google Cloud, AWS, Azure, they all offer VMs, object stores, databases, functions, etc.

So the foundation of cloud computing is the same across all cloud providers.

Differences however may be:

- Pricing
- Performance
- Features
- How you interact with the service
- Etc.

## Functions as services

Cloud providers also offer you the ability to run code without having to worry about the underlying infrastructure. This is known as Functions as a Service (FaaS).

They let you run compute without worrying. This is built on top of CPU. So if you're not concerned about disk and just want to run code, this is what you'd use e.g. AWS Lambda, Google Cloud Functions, Azure Functions.

This is also an example of managed service. When people refer to serverless, this is what they're talking about. It's the highest level of abstraction. You just write code, and the cloud provider takes care of the rest.

## That's actually enough

You will typically not even need to deal with VMs. An object store for files, database and functions is enough for most applications. With these three services, you can build a lot of things already.

## Observability

When you're running your application in the cloud, you will want to know what's going on. You will want to know how many requests are coming in, how long they're taking, how much memory you're using, etc. That's where observability comes in.

Logging: You will want to log what's happening in your application. This can help you debug issues in production and understand what's going on, e.g. if a user complains that something isn't working.

Monitoring: You will want to monitor your application. You will want to know if your application is up or down, if it's slow (how long queries are taking), if it's using too much memory, etc.

Alerts: You will want to be alerted if something goes wrong, e.g. if you're hitting more 400 errors than usual, latency is too high, etc.

Cloud providers offer you services to help you with observability. For example, AWS CloudWatch, Google Cloud Monitoring, Azure Monitor.

However, there are popular services that fully focus on observability. Datadog is very a popular one.

## Data warehouses

Data warehouses are a type of database that are optimized for analytics. They're not for transactional data, but for running complex queries over large amounts of data. They're often used by data analysts and data scientists to run queries and generate reports.

They're often used by companies to run complex queries over large amounts of data. For example, a company might want to know how many users are using a certain feature, or how many users have bought a certain product.

Cloud providers offer you managed data warehouses. For example, AWS Redshift, Google BigQuery, Azure Synapse Analytics.

However, here external services are also popular. For example, Snowflake, Databricks, etc.

## Cloud wrappers

Cloud wrappers are services that make it easier to work with cloud providers. They're often used by developers to deploy their applications to the cloud. People still often complain about how it's hard to work with cloud providers, and that's where cloud wrappers come in.

Popular ones include Vercel and Netlify. They make it easy to deploy your application to the cloud. You just run a command, and your application is deployed.

## Regional vs Global services

Some services are regional, and some are global. Regional services are usually cheaper, but they're not always available in all regions. Global services are available in all regions, but they're usually more expensive.

A CDN is inherently a global service, because you've got servers all over the world where you want to cache your static content. So you can't really have a regional CDN.

VMs are regional. You can't just have a VM that's split across multiple regions. You have to specify the region when you create the VM.

It gets a bit fuzzy when talking about services like DynamoDB, Google Cloud Spanner, etc.

RDS for example is primarily a regional service. This means when you deploy RDS instance, it is deployed in a single region. However, you can create read replicas in other regions. This is a way to make it more highly available, but it's not the same as a global service.

DynamoDB can be considered a global service. You can create a table in a single region, and then enable global tables. DynamoDB Global Tables provide a fully managed, multi-region, and multi-active database option that delivers fast, localized read and write performance for massively scaled, global applications.
