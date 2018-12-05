# Alertmanager

This is a tutorial on how to launch and manage a fully working Alertmanager cluster in AWS.

The notes are also posted on the [NETBEARS](https://netbears.com/blog/monitoring-alerting-prometheus-aws/) company blog. You might want to check the website out for more tutorials like this.

## What is Alertmanager?

[Alertmanager](https://prometheus.io/docs/alerting/alertmanager/) handles alerts sent by client applications such as the Prometheus server. It takes care of deduplicating, grouping, and routing them to the correct receiver integration such as email, PagerDuty, or OpsGenie. It also takes care of silencing and inhibition of alerts.

Alertmanager's main features are:
1. __Grouping__: Grouping categorizes alerts of similar nature into a single notification. This is especially useful during larger outages when many systems fail at once and hundreds to thousands of alerts may be firing simultaneously.
2. __Inhibition__: Inhibition is a concept of suppressing notifications for certain alerts if certain other alerts are already firing.
3. __Silences__: Silences are a straightforward way to simply mute alerts for a given time. A silence is configured based on matchers, just like the routing tree. Incoming alerts are checked whether they match all the equality or regular expression matchers of an active silence. If they do, no notifications will be sent out for that alert.
4. __High Availability__: Alertmanager supports configuration to create a cluster for high availability. This can be configured using the --cluster-* flags.

## Deploy the stack

### Run the CloudFormation template in the AWS Console
* Login to the AWS console and browse to the CloudFormation section
* Select the cloudformation-template.yaml file
* Before clicking "Create", make sure that you scroll down and tick the “I acknowledge that AWS CloudFormation might create IAM resources” checkbox
* ...drink coffee...
* Go to the URL in the output section for the environment that you want to access

### Main resources created

* 1 AutoScaling Group
* 1 Elastic Load Balancer
* 1 DNS record (for ease of access)

### Monitoring

The stack launches [NodeExporter](https://github.com/prometheus/node_exporter/) (Prometheus exporter for hardware and OS metrics exposed by NIX kernels, written in Go with pluggable metric collectors) on each host inside the cluster.

## Final notes
Need help implementing this?

Feel free to contact us using [this form](https://netbears.com/#contact-form).
