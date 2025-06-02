# Introduction lab exercises

Welcome to the Advanced Querying lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about Elastic Security.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Ingesting Zeek logs in Elasticsearch
- Executing KQL queries to filter documents
- Develop ES|QL queries for playing with DNS, URLS and enriching the data set
- Use EQL to investigate a Security incident
- Inspect an Elastic Security panel to identify ECS dependencies

## Exercise 1 - Executing KQL queries to filter documents

This first exercise you are going to work with Kibana Query Language (KQL). During the exercise you are going to answer the questions below to solve the security incident related to a Data theft. For these labs we need to import the logs that are captured using Zeek.

### 1.1 - Ensure that the Zeek host logs are ingested into Elastic Security

To achieve this, we can adjust our *elastic_agent* container to mount the logs and deploy the Zeek Integration. Another way is spinning up a Zeek container. Decision is yours.

Just bind the logs to the `elastic-agent` container, in the `docker-compose.yml` file.

Add this rule below `- "/:/hostfs:ro"`
```
      - "./zeek/logs/:/var/log/bro/current:ro"
```

Or the hard way. Run an `elastic-agent` container called `zeek-host` and run `docker compose up` again.

Ensure that the `zeekdata` volume is defined under volumes, in the `docker-compose.yml` file.

```
  zeekdata:
    driver: local
```

And add the zeek-host to the `docker-compose.yml` file.

```
zeek-host:
    depends_on:
      fleet-server:
        condition: service_healthy
    image: docker.elastic.co/beats/elastic-agent:${STACK_VERSION}
    hostname: docker-zeek-host
    volumes:
      - certs:/certs
      - zeekdata:/usr/share/elastic-agent
      - "/var/lib/docker/containers:/var/lib/docker/containers:ro"
      - "/var/run/docker.sock:/var/run/docker.sock:ro"
      - "/sys/fs/cgroup:/hostfs/sys/fs/cgroup:ro"
      - "/proc:/hostfs/proc:ro"
      - "/:/hostfs:ro"
      - "./zeek/logs/:/var/log/bro/current:ro"
    ports: []
    user: root
    environment:
      - FLEET_CA=/certs/ca/ca.crt
      - FLEET_ENROLL=1
      - FLEET_INSECURE=true
      - FLEET_URL=https://fleet-server:8220
      - KIBANA_FLEET_HOST=https://kibana:5601
      - KIBANA_HOST=https://kibana:5601
      - KIBANA_FLEET_CA=/certs/ca/ca.crt
      - ELASTICSEARCH_USERNAME=elastic
      - ELASTICSEARCH_PASSWORD=${ELASTIC_PASSWORD}
      - FLEET_TOKEN_POLICY_NAME=Linux-Agent-Policy
``` 

enjoy this first exercise.

#### 1.2 - Deploy the Zeek Integration to Linux-Agent-Policy

- Open Kibana
- Under Management, open Integrations
- Search for the Zeek integration and click this to open
- Top-right click 'Add Zeek'
- Read through the default configuration and validate '/var/log/bro/current' is monitored.
- Choose existing hosts and select the `Linux-Agent-Policy`
- Save and continue
- Yes, Save and Deploy changes

Now the integration is being deployed and activated.

Can you check what `time-period` events are ingested? Use the [Logs] Zeek overview dashbboard under Assets.

### 1.3 - Write a KQL query that only return Zeek events.

Create a query that only returns documents that are ingested by Zeek.

- Query must be in KQL.
- Query must be as simple as possible.
- Result must only contain Zeek Integration events.

### 1.4 - Identify the IP address that is used to upload the customer data to an Port 443 location.

Create a query that only returns documents that are ingested by Zeek, related to Network and used Port '443' to upload the data.

- Query must be in KQL.
- Query must be as simple as possible.
- Result must only contain Zeek Integration events.

Write down the ip address (`host.ip`) you resolved.

### 1.5 - Gather all related events from host.ip and return all hits excluding when destination is set to 127.0.0.1

Great that you found the initiating 'host.ip'. Let's find out which services it was using.

Create a query that only returns documents that are ingested by Zeek, related to the `host.ip`. Exclude when the `destination.ip` is set to 127.0.0.1.

- Query must be in KQL.
- Query must be as simple as possible.
- Result must only contain Zeek Integration events.

Write down the query for the documents. Your colleague is going to analyze these again.


### 1.6 - Filter events only that have a destination in the countries United States and Sweden. 

*Hint: Use the ISO Country codes for filtering.*

List with documents really helped me. I still beginning to learn KQL. Can you filter only documents that have a destination in Sweden or the United States?

Create a query that only returns documents that are ingested by Zeek, related to the `host.ip`. Exclude when the `destination.ip` is set to 127.0.0.1 and have set `country_iso_code` set to either US or SE.

- Query must be in KQL.
- Query must be as simple as possible.
- Result must only contain Zeek Integration events.

Write down the query for the documents. Your colleague is going to analyze these again.

### 1.7 - Filter event that orig

*Hint: Think about excludes*

You got cake ! Those three events helped him to remove some surrounding events related to your current Cloud provider Akamai and a secure connection. He shared with you his last KQL query.

Can you write down this query, which is an extend on your current query
- Ensuring only non-secure Web ports are included.
- We exclude the `destination.ip` from Akamai.

- Query must be in KQL.
- Query must be as simple as possible.
- Result must only contain Zeek Integration events.

Write down the query for the documents. You should only have one document that returns.

## Exercise 2 - ES|QL Queries for fun, analysing System events and parsing with advanced workflows

This exercise we are going to play around with ES|QL. We start easy, but try to include some more advanced examples. Let's start.

### 2.1 - Open the ES|QL Console and show the last 10 events

- Open Kibana, Discover
- Click top-right on Try ES|QL

Now get the last 10 events from `logs-*`.

### 2.2 - Create a query that counts all events last 30 seconds

- Query must be in ES|QL.
- Query must be piped over multiple lines for readability.
- Ensure that DESC is selected.

```
FROM logs-*
| WHERE @timestamp > NOW() - 30 second
| STATS COUNT(*)
```

Can you try ASC and for last hour?

### 2.3 - Query events where host.name start with docker and show the total_events per agent.name

- Query must be in ES|QL.
- Query must be piped over multiple lines for readability.
- Ensure that DESC is selected.

Try out the query. Which agents are shown?

- Examine the output.
- Review the query and look if you can play around with changing the WHERE clause.

```
FROM logs-*
| WHERE host.name LIKE "docker*"
| STATS total_events = COUNT() BY agent.name
| KEEP agent.name, total_events
```

### 2.4 - Parse a log based on an advanced workflow

- Query must be in ES|QL.
- Query must be piped over multiple lines for readability.

Which advanced workflow will you use? 

Either GROK or DISSECT. You get the DISSECT for free, now you have to develop the GROK code snippet.

```
ROW logentry = "2025-06-02T12:15:00.000Z - ghost - 192.168.30.1"
| DISSECT logentry """%{@timestamp} - %{host.name} - %{ip.address}"""
| KEEP @timestamp, host.name, ip.address
```

### 2.5 - Calculate the total sessions per interface for Podman.EXE

- Query must be in ES|QL.
- Query must be piped over multiple lines for readability.

Can you create a query this query from scratch?

- Examine the output.
- Review the query and look if you can change this for other processes.

```
FROM logs-*
| WHERE process.pid IS NOT NULL
| WHERE process.name == "podman.exe"
| STATS total_sessions = COUNT_DISTINCT(host.ip) BY host.ip
| KEEP total_sessions, host.ip
```

## Exercise 3 - Use EQL to investigate a Security incident 

This exercise you are going to use Elastic Query Language (EQL).  We are going to investigate a Security incident related to `elastic-agent.exe`. Seems to be a ambigious process.

For this exercise you have to use `Dev Tools`.

 - Open Dev Tools under Management

### 3.1 - Get a list of elastic-agent.exe process events

Search for all `elastic-agent.exe` process events. Additional you can minimize the total events to 10 events.

```
GET /logs-*/_eql/search
{
  "query": """
    process where process.name == "elastic-agent.exe"
  ""“,
  “size”: 10
}
```

### 3.2 - Get a series of ordered events executed by elastic-agent.exe

Search for all `elastic-agent.exe` process events that are followed by a file events regarding `PowerShell` script executions.

```
GET /logs-*/_eql/search
{
  "query": """
    sequence
      [ process where process.name == "elastic-agent.exe" ]
      [ file where stringContains(file.name, "*.ps1") ]
  """
}
```

- Examine the output.
- Try to introduce a time-span. `sequence with maxspan=10ms`
- Review the query and look if you can change this for registry events.

## Exercise 4 - Inspect an Elastic Security panel to identify ECS dependencies

Sometimes data is not showing up in Elastic Security. This can be related to data model dependencies. Try to look which query is used to populate *Uncommon processes* shown at the Hosts Overview.

- Open Explore under Security.
- Open Hosts.
- Scroll to Uncommon processes.
- At the top-right click the Inspect icon.
- Copy over the Request.
- Examine the output and find out which ECS fields are used.

Try this exercise also for Network panels.

## Next Steps

You are ready to start with the lab about [Advanced Alerting](../06-AdvancedAlerting/README.md) for Elastic Security. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!