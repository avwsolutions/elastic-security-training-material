# Labs Introduction

These labs will give the full experience of deploying, discover, visualize, creating detection-rules and more using Elastic Security. Every lab contains several exercises to complete.

If you are unable to complete certain exercises, no problem. You can always complete the other labs.

## Labs

| #   | Lab Name                                                                             | Description                                                                                                                                                                                                                                                                             |
|------|--------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0   | [Prerequisites](00-prereqs/README.md) | Prereqs to setup the environment|
| 1   | [Introduction](01-introduction/README.md)| In this lab during the exercises attendees will learn howto spin-up a full Elastic-Stack using Docker containers.|
| 2   | [Elastic Stack as Fundament](02-StackFoundation/README.md) | In this lab during the exercises attendees will learn about the Elastic Stack foundations, such as Kibana and Spaces.|
| 3   | [Advanced Ingestion Tools](03-AdvancedIngestion/README.md) | In this lab during the exercises attendees will learn about advanced ingestion capabilities like elastic agent, beats, logstash and more.|
| 4   | [Detections & Alerts](04-DetectionsAlerts/README.md) | In this lab during the exercises attendees will learn about detections, detection-rules, alerts and optimizing to prevent False-Positives and detection-rule optimalization/tuning.|
| 5   | [Advanced Query Tools](05-AdvancedQuerying/README.md) | In this lab during the exercises attendees will learn about adanced query languages like KQL, Lucene, ES|QL and EQL. We also look at the ECS.|
| 6   | [Advanced Alerting](06-AdvancedAlerting/README.md) | In this lab during the exercises attendees will learn about advanced alerting like connectors, actions, case creation and templates.|
| 7   | [Dashboards](07-Dashboards/README.md) | In this lab during the exercises attendees will learn about dashboards, creating your own dashboards and exporting them.|
| 8   | [Advanced Investigation](08/AdvancedInvestigation/README.md) | In this lab during the exercises attendees will learn about investigation tools, like built-in from Elastic, others like OSQuery, Sysmon and using Threat Intelligence.|
| 9   | [Cloud Security](09-CloudSecurity/README.md) | In this lab during the exercises attendees will learn about Cloud Security Posture Management and Cloud Vulnerability Management with Trivy.|
| 10   | [EDR with Elastic Defend](10-EDRDefend/README.md) | In this lab during the exercises attendees will learn about EDR with Elastic Defend, configuring the integration, creating event lists and integrate with Microsoft Defender.|
| 11   | [Advanced Entity Analytics](11-AdvancedAnalytics/README.md) | In this lab during the exercises attendees will learn about Advanced Entity Analytics, which uses Elastic ML and can help to calculate entity risk scores and managee your asset risk within Elastic.|

## Prerequisites

You may use any `Elastic Stack` environment, but as minimum we advice the following prerequisites that are part of [Lab 0](00-prereqs/README.md). For simplicity we are making use of a demo deployment using `Docker compose`. Keep in mind this is for training purposes only!!

- 2 or more (virtual) CPUs available.
- At least 16G of Memory.
- Approx 5 GB available for storage.

** This training is developed and tested using Elastic Stack 8.17.4 release **

## Next Steps

You are ready to start with the first lab about [Prerequisites](00-prereqs/README.md) setting up Elastic Stack with Podman Compose.

Enjoy the exercises!!!