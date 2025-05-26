# Introduction lab exercises

Welcome to the Elastic Stack as Advanced Ingestion lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about Elastic Security.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Setup Sysmon
- Enable enrichment
- Activate Threat Intelligence

## Exercise 1 - Setup Sysmon collector

This first exercise you are going to setup the Sysmon collector. This helps to generate more usable traffic.

Open a PowerShell 7 Administrator run-as terminal

```
sysmon -accepteula -i content\sysmonconfig-export.xml
```

Now reconfigure the Windows Integration to include Sysmon Operational.

## Exercise 2 - Enable enrichment

This exercise we are going to enable enrichment.

### 2.1 - Add the initial asset table

```
PUT /assets/_doc/1?refresh=wait_for
{
  "name": "<your-host-name>",
  "description": "Windows lab environment",
  "owner": "<your-fake-name>",
  "score": "100",
  "unit": "training"
}
```

### 2.2 - Add the initial asset-policy for enrichment

```
PUT /_enrich/policy/asset-policy
{
  "match": {
    "indices": "assets",
    "match_field": "name",
    "enrich_fields": ["name", "description", "owner", "score" ]
  }
}
```

### 2.3 - Enable the asset-policy

```
POST /_enrich/policy/asset-policy/_execute?wait_for_completion=false
```

### 2.4 - Create an asset_lookup pipeline

```
PUT /_ingest/pipeline/asset_lookup
{
  "processors" : [
    {
      "enrich" : {
        "description": "Lookup assets",
        "policy_name": "asset-policy",
        "field" : "host.name",
        "target_field": "asset",
        "max_matches": "1"
      }
    }
  ]
}
```

## 2.5 - Extend Elastic Agent Normalization with asset enrichment

```
PUT _ingest/pipeline/logs-elastic_agent@custom
{
  "processors": [
    {
      "pipeline": {
        "name": "asset_lookup",
        "ignore_missing_pipeline": true,
        "tag": "enrich"
      }
    }
  ]
}
```

## 2.6 - Test enrichment and look if assets are enriched

- Open Kibana console
- Filter for host.name: specific event.
- Look if the specific host events are enriched.
- Try to add another asset entry to enrich.


