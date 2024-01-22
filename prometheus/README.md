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

## Metrics

Prometheus uses a multi-dimensional data model with time series data identified by metric name and key/value pairs. This data model is very flexible and allows you to create metrics with multiple dimensions, which is very useful for monitoring systems.

### Metric types

Prometheus has four metric types:

- **Counter:** A counter is a cumulative metric that represents a single numerical value that only ever goes up. It can be used to represent the number of requests served, tasks completed, or errors.

- **Gauge:** A gauge is a metric that represents a single numerical value that can arbitrarily go up and down. Gauges are typically used for measured values like temperatures or current memory usage, but also "counts" that can go up and down, like the number of concurrent requests.

- **Histogram:** A histogram samples observations (usually things like request durations or response sizes) and counts them in configurable buckets. It also provides a sum of all observed values.

- **Summary:** Similar to a histogram, a summary samples observations (usually things like request durations and response sizes). While it also provides a total count of observations and a sum of all observed values, it calculates configurable quantiles over a sliding time window.

## PromQL

Prometheus provides a functional query language called PromQL (Prometheus Query Language) that lets the user select and aggregate time series data in real-time. It is a very powerful language that allows you to query and aggregate metrics in many different ways and it is the main way to query and visualize metrics in Prometheus.

Example of a PromQL query:

```bash
http_requests_total{job="my-service", method="GET"}
rate(http_requests_total[5m])
http_requests_total{status="500"}
```

## Running locally

```bash
docker-compose up -d
```