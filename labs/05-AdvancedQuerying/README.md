# Introduction lab exercises

Welcome to the Advanced Querying lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about Elastic Security.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Ingesting Zeek logs in Elasticsearch
- Executing KQL queries to filter documents
- Develop ES|QL queries for enriching a data set
- Use EQL to investigate a Security incident
- Inspect an Elastic Security panel to identify ECS dependencies

## Exercise 1 - Executing KQL queries to filter documents

This first exercise you are going to work with Kibana Query Language (KQL). During the exercise you are going to answer the questions below to solve the security incident. For these labs we need to import the logs that are captured using Zeek.

To achieve this, we can adjust our *elastic_agent* container to mount the logs and deploy the Zeek Integration. Another way is spinning up a Zeek container. Decision is yours.

Just bind the logs to the `elastic-agent` container.

Add this rule below `- "/:/hostfs:ro"`
```
      - "./zeek/logs/:/var/log/bro/current:ro"
```

The hard way.

Ensure that the `zeekdata` volume is defined under volumes.

```
  zeekdata:
    driver: local
```

And add the zeek-host.

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


```


- Create a KQL query that 

- Open Rules under Security
- Click Add integrations in the top-right
- Search for prebuilt Security
- Click Prebuilt Security Detection Rules to open
- Click add Prebuilt Security Detection Rules
- Add them to your Linux-Agent-Policy

Now all latest pre-built rules are available. Now try to enable a rule called whoami.exe and try to catch an alert.

```
psexec -s powershell whoami.exe /user
psexec -s cmd /c whoami.exe /groups 
```

## Exercise 2 - Duplicate pre-built rule for customization

Try to edit the pre-built rule. This isn't possible. Best practice is to duplicate and add your company specifics to tune and ensure to reduce false positives.

- Lookup the nping rule.
- Click on the three dots to Duplicate rule.
- Choose only the rule.
- Now enable the rule.
- Which Integration is required to catch those events?

## Exercise 3 - Create a Custom Query detection-rule

This exercise we are going to create a custom query detection rule. Here we are going to monitor calc.exe for educational purposes only.

- Open Rules under Security
- Click create new rule
- Choose Custom query
- Query is process.name : calc.exe
- Add alert suppression using host.name.
- Add a name Calc.exe started with description Process can harm your employees.
- Severity is Low
- Add a schedule of 1m/1m lookback.
- No action for now.

Now do a rule preview. Don't forget to start calc.exe to see the results.

## Next Steps

You are ready to start with the lab about [Advanced Querying](../05-AdvancedQuerying/README.md) for Elastic Security. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!