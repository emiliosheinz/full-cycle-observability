## Initial Concepts

There are two main ways of monitoring a system: **pull-based** and **push-based**. In the pull-based model, the monitoring system periodically connects to the system being monitored and requests metrics and logs. In the push-based model, the system being monitored periodically sends metrics and logs to the monitoring system. Prometheus uses the pull-based model through http, while Elastic Stack uses the push-based model, that is one of the main differences between them.

![Push and Pull diagram](./docs/push-pull.png)

## Exporters

Prometheus leverages exporters to gather metrics from diverse systems and services, transforming them into a format intelligible to Prometheus. These exporters cover a broad spectrum, including specialized ones for MySQL, Nginx, Redis, and numerous others. Additionally, users have the flexibility to craft custom exporters tailored to their specific requirements.

We can understand the exporter as an interface between the system being monitored and Prometheus. Like exemplified below, it is responsible for collecting metrics from the system and exposing them in a format that Prometheus can understand.

![Exporter diagram](./docs/exporters.png)

## Architecture

This diagram illustrates the architecture of Prometheus and some of its ecosystem components:

![Prometheus architecture](./docs/prometheus-architecture.png)

Prometheus scrapes metrics from instrumented jobs, either directly or via an intermediary push gateway for short-lived jobs. It stores all scraped samples locally and runs rules over this data to either aggregate and record new time series from existing data or generate alerts. Grafana or other API consumers can be used to visualize the collected data.

### Prometheus Server

The Prometheus server is the core piece of Prometheus architecture. It is responsible for collecting metrics from the configured jobs, processing and storing them. It also provides a web interface where you can run queries and visualize the collected data.

- **TSDB (Time Series Database):** Is the storage layer of Prometheus where a custom database written on top of LevelDB is used for storing and querying time series data, which makes it very efficient to store and query large amounts of data.

- **Retrieval:** The retrieval component is responsible for collecting and orchestrating metrics from the configured jobs and applying the configured rules to them.

- **HTTP Server:** The HTTP server is responsible for serving the web interface and API for querying and visualizing the collected data.

### Service discovery

Prometheus supports multiple service discovery mechanisms, including static and dynamic ones. The static service discovery is the simplest one, where you have to manually configure the list of targets to be monitored. The dynamic service discovery is more complex, but it is also a more flexible and scalable solution. To implement a dynamic service discovery Prometheus can be connected to a Kubernetes cluster, for example, and it will automatically discover and monitor all the pods that match the configured criteria.

### Push Gateway

The push gateway is an intermediary service that allows you to push metrics from short-lived jobs to Prometheus. It is useful for monitoring batch jobs, for example, where the job is completed before Prometheus scrapes the metrics. The push gateway is not recommended for long-lived jobs because it will store all the metrics in memory, which can cause memory issues.

### Alertmanager

The Alertmanager is responsible for handling alerts sent by Prometheus. It can group alerts, silence them for a given period, and send them via email, Slack, PagerDuty, and other notification channels.

### Grafana

Grafana is an open-source visualization tool that can be used to query, visualize, and alert on metrics collected by Prometheus. It is a very powerful tool that can be used to create dashboards and alerts for monitoring systems.