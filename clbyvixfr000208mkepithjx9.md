# Monitoring Made Easy with Prometheus




#  Site Reliability Engineering 

Site reliability engineering (SRE) is a discipline that combines software engineering and operations to ensure the reliability and scalability of a system. Google first applied it in 2003 to enhance the reliability of the company's systems and services.

At the time, Google's systems were rapidly expanding at the time, and the company was facing increasing challenges in maintaining their dependability. To address this, Google formed a team of engineers in charge of both developing and operating the systems. Site reliability engineers were the title given to these engineers (SREs)!


Google's SRE team was primarily in charge of:
- Monitoring the systems 
- Automating tasks
- Responding to incidents.

They also worked to continuously improve the systems' reliability and scalability by modifying the architecture and introducing new tools and technologies. 


SRE has gained widespread acclaim in the tech industry since its inception. Many businesses now have SRE teams in place to ensure the reliability of their systems and services. Other disciplines, such as site reliability architecture (SRA) and site reliability management, have been inspired by SRE (SRM).

I recommend this Google resource for more on SRE: [https://sre.google/](https://sre.google/)


## SRE, Essential Principles

SRE's goal is to improve system performance by applying engineering principles to its operations, which are listed below:


- **Automation is key:** SRE teams use automation to perform tasks that are repetitive, error-prone, or time-consuming. This allows them to focus on more important tasks and helps to reduce the risk of human error.

- **Error budgets:** SRE teams allocate a certain percentage of their time to proactive tasks such as improving the system's reliability, and the rest of the time is reserved for reactive tasks such as responding to issues. This is known as an error budget, and it helps the team prioritize tasks and ensure that the system remains reliable over time.

- **Use of data:** SRE teams rely heavily on data to understand the performance of the system and identify patterns or trends that may indicate a problem. They use tools such as application performance monitoring (APM) tools, infrastructure monitoring tools, and log analysis tools to collect and analyze data.

- **Continuous improvement:** SRE teams are focused on continuously improving the reliability and scalability of the system. This can involve implementing changes to the system's architecture, introducing new tools and technologies, or redesigning processes to make them more efficient.

- **Reliability is a feature:** SRE teams view reliability as a critical feature of the system, and they prioritize it accordingly. They use a variety of **tools and techniques** to monitor the system and detect issues, and they take action to prevent outages and improve the overall reliability of the system.


**Promethus**, the CNCF open source project, is one of the leading monitoring systems. Let's get begin!


# Get to Know Promethus

Prometheus is a time series database  monitoring system, Yes, once again, the result of an open-source-driven community. The development of Prometheus has been heavily influenced by the community, and it continues to be an actively developed and supported project.


SoundCloud engineers created Prometheus in 2012 as a way to monitor the performance of their systems and services. It gained popularity quickly and was adopted by other organizations. The CNCF approved it as a project in 2015, and it has since been actively developed and maintained by a large community of users and contributors.

Prometheus' development is guided by a set of principles that prioritize simplicity, robustness, and usability. It is intended to be scalable and capable of handling large amounts of data as well as a high volume of queries. It also has a set of integrations with other tools and systems, making it simple to use in a variety of settings.

Let us explain what makes it a worthwhile consideration!

## Features For Your Note

Prometheus has several key features that make it an appealing choice, incl:

- **Flexible query language:** Prometheus has a powerful query language that allows users to define custom metrics and alerts based on their specific needs.

- **Time series database:** Prometheus stores metrics in a time series database, which allows users to view and analyze the data over time to understand trends and identify patterns or anomalies.

- **Scraping:** Prometheus can scrape metrics from target systems, which means it can periodically retrieve metrics from other systems and store them in its time series database.

- **Alerting:** Prometheus has built-in alerting capabilities that allow users to define alert rules based on metric thresholds or other conditions. When an alert is triggered, it can send notifications to the user or trigger an automatic response.

- **Integrations:** Prometheus has a rich set of integrations with other tools and systems, which makes it easy to use in a variety of environments. It is often used in conjunction with tools such as **Grafana** and **Kubernetes**.

- **Scalability:** Prometheus is designed to be scalable and can handle large amounts of data and a high volume of queries.


## Workflow Prior To The Jump


1- Install Prometheus: You can install Prometheus on your own server or use a managed service such as Prometheus as a Service.

2- Configure Prometheus: After installing Prometheus, you will need to configure it to collect metrics from the target systems and applications that you want to monitor. You can do this using configuration files and command-line flags.

3- Set up targets: To collect metrics, Prometheus needs to know which systems and applications to scrape for data. You can set up targets using configuration files or the Prometheus web interface.

4- Set up alerts: Prometheus includes a powerful alerting system that allows you to set up rules and notifications for any kind of behavior or anomaly. You can set up alerts using configuration files or the Prometheus web interface.

5- Visualize and analyze data: Prometheus includes a flexible query language and a range of visualization tools that allow you to analyze and understand your metrics data. You can use these tools to create graphs, dashboards, and alerts.



# The Jump
The following is an outline of the steps to install Prometheus on a Linux-based system as are the majority of servers.


1- Download the latest release of Prometheus from the [official Prometheus website](https://prometheus.io/download/). You can either download a pre-built binary or build Prometheus from source.

2- Extract the downloaded archive and navigate to the directory containing the Prometheus executable.


## Create a configuration file for Prometheus. 

You can use the prometheus.yml.example file as a starting point and customize it to suit your needs. Or you can create your just right now! 

You will need to create a`  .yml`  file that specifies the configuration options for your Prometheus server. Here are guidelines for creating a configuration file for Prometheus:


1- Begin the file with ` global`  and ` scrape_configs`  blocks. The ` global`  block allows you to specify global configuration options that apply to all scrape jobs, while the ` scrape_configs`  block specifies individual scrape jobs and the targets they should scrape.


2- In the `global block`, you can specify options such as the external labels that should be applied to all metrics, the retention period for data, and the frequency at which the Prometheus server should scrape targets.

3- In the `scrape_configs` block, you can specify individual scrape jobs using the `- job_name` option. For each scrape job, you will need to specify the targets to scrape using the `static_configs` or `file_sd_configsv options. You can also specify additional options such as the scrape interval and the metrics path.

4- Save the file with a .yml extension and use the `--config.file` flag to specify the path to the configuration file when starting the Prometheus server.

Here is an example of a simple Prometheus configuration file:

```
global:
  external_labels:
    env: production
  retention: 90d
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']


```


This configuration file specifies two scrape jobs: one for the Prometheus server itself and one for the node exporter. It also specifies a global retention period of 90 days and a scrape interval of 15 seconds.

5- Start the Prometheus server using the following command:

``` ./prometheus --config.file=<path to your config file> ```



That's it! GreatJob. You can verify that Prometheus is running by visiting http://localhost:9090 in your web browser. The Prometheus UI should now be accessible.

Start your monitoring Journey, at this level, you can proceed doing the following:
- Set up alerts and create Alert rules.
-  Visualize and analyze data.
-  Monitor Third party Applications
- Collect Metrics 

Whether you are just getting started with monitoring or are looking to improve your existing monitoring practices, **Prometheus** is definitely worth considering.

# Synopsis

That should do it for today! I had the pleasure of taking you to a great discipline that I enjoy doing, SRE!


While SRE and DevOps have different focuses, they often overlap in practice and can be complementary to each other.  SRE teams may use DevOps practices such as continuous delivery and automation to improve the reliability of the system. Similarly, DevOps teams may adopt SRE principles such as error budgets and monitoring to ensure the reliability and performance of the system.

The moral, don't limit yourself to a specific job role; be curious and strive to learn as much as you can in order to provide value to your team and organization. and eventually the world.

























