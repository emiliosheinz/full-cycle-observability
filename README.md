# Full Cycle Observability

Modern systems are like airplanes, they are complex and have many moving parts. Would you fly in an airplane that doesn't have a observability? I wouldn't. The same goes for software systems, we need to have a way to monitor our systems and understand what is happening inside them so that we can make informed decisions when something goes wrong.

Observability is a measure of how well internal states of a system can be inferred from knowledge of its external outputs. It helps us understand what is happening inside a system from the outside and is key to building reliable, scalable, and maintainable systems, specially in a microservices architecture or in big monoliths.

## Observability vs Monitoring

Observability and monitoring are closely related concepts in the realm of software development and system management. Monitoring traditionally focuses on collecting and analyzing specific metrics and data points to ensure the health and performance of a system. It often involves setting up predefined thresholds and alerts for key indicators. On the other hand, Observability is a more holistic approach that emphasizes understanding and debugging complex systems by gaining insights into their internal states and behaviors. Observability goes beyond traditional monitoring by providing the ability to ask ad-hoc questions, explore system behavior in real-time, and correlate events across distributed components. While monitoring helps identify issues, observability aids in understanding the root causes of problems and enables more effective troubleshooting in dynamic and interconnected systems. Together, they play essential roles in maintaining the reliability and performance of modern software applications.

## The Three Pillars of Observability

The three pillars of observability are: **metrics**, **logs**, and **traces**. They are the building blocks of observability and are the key to understanding what is happening inside a system.

### Metrics

Metrics are a way to measure and quantify the behavior of a system. They are usually numerical values that can be aggregated and analyzed over time. Metrics are the most common way to monitor systems and are the foundation of many monitoring tools. They are also the most common way to alert on system behavior like CPU usage, memory usage, and disk space usage for example.

### Logs

Logs are a way to record events that happen inside a system. They are usually text messages that contain information about what happened, when it happened, and where it happened. Logs are the most common way to debug systems and differently from metrics, they are not aggregated and analyzed oer time. Not correctly using logs can lead to a lot of problems like not having enough information to debug a problem that is happening in production.

### Traces

Traces are a way to record the lifecycle of a request as it flows through a system. They are usually composed of multiple spans that represent different operations that happened during the request lifecycle. Traces are the most common way to debug distributed systems and are key to understanding how requests are flowing through a system and how a system is behaving as a whole.

## Elastic Stack

The Elastic Stack is basically the ELK Stack plus Beats. Beats are lightweight data shippers that you install as agents on your servers to send specific types of operational data to Elasticsearch. Beats are the data collection component of the Elastic Stack and are responsible for collecting data from your servers and sending it to Elasticsearch.

[Read more amore about Elastic Stack >](./elastic-stack/README.md)

## Prometheus

Prometheus is an open-source systems monitoring and alerting toolkit originally built at SoundCloud. Since its inception in 2012, many companies and organizations have adopted Prometheus, and the project has a very active developer and user community. It is now a standalone open source project and maintained independently of any company. To emphasize this, and to clarify the project's governance structure, Prometheus joined the Cloud Native Computing Foundation in 2016 as the second hosted project, after Kubernetes.

[Read more amore about Prometheus >](./prometheus/README.md)