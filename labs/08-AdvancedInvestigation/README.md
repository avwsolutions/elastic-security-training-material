# Introduction lab exercises

Welcome to the Advanced Investigation lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about Elastic Security.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Exploring Elastic Security features
- Enabling threat Intelligence
- Schedule a query using OSQuery
- Add your custom Threat Intelligence

## Exercise 1 - Exploring Elastic Security features

This first exercise is about understanding the way how Elastic optimizes triage. Most tools have the UI setup in a way you can go from left through the right, getting into more into evidence collection.

- Use Explore insights to spot anomalies in your host, network and Users behaviour.
- On User insights, click all users
- Select a user of choice to dive into.
- To investigate further add the user to a timeline.
- Analyse the surrounding events and look into alerts using the visual event analyzer.
- Now save your timeline and add this to a new case.

Give it a try. How would you approach this triage?

## Exercise 2 - Enabling threat Intelligence

This exercise you may need a free account at AbuseCH. Just create one and retrieve your personal API Key.

- Open Integrations.
- Search for AbuseCH
- Click Add AbuseCH
- Click on default settings and add your personal Auth Key.
- Now deploy this integration to the Linux_Agent_Policy.
- Open Intelligence under Security.

Examine the TI data that is coming in from AbuseCH. Just enabled this.

Additional exercise is to lookup TI detection rules and enable them for all IoC that are collected.

## Exercise 3 - Schedule a query using OSQuery

You already have seen an OSQuery container running. Here we can easily run queries.

- We run queries using osqueryi
- We schedule queries using osqueryd

Now let's dive into the first exercise

### 3.1 - Install Integration for OSQUery Logs and Lookup OSQuery Events

Examine if the scheduler already ingests osquery events. For this you must deploy the OSQuery Logs Integration to the *Linux-Agent-Policy*.

- Open Analytics.
- Search for event.module: "osquery" 

### 3.2 - Look OSQuery scheduled events configuration

- Open a bash in the OSQuery container
```
docker exec -it es-cluster-osquery-1 bash
``` 
- Now do `more osquery.conf`

The following schedule is shown.
```
 "schedule": {
    // This is a simple example query that outputs basic system information.
    "system_info": {
      // The exact query to run.
      "query": "SELECT hostname, cpu_brand, physical_memory FROM system_info;",
      // The interval in seconds to run this query, not an exact interval.
      "interval": 3600
    },
    "processes": {
       "query": "SELECT * FROM processes;",
       "interval": 3600
    }
  },
  ```

### 3.3 - Schedule your own event with OSQuery

Now try to add your own query. Ensure that you first install `vim`

```
apt update -y
apt install vim -y
```

Add the following. If the container fails, then you may have issues with the syntax.

```
,
    "passwdhash": {
       "query": "SELECT md5 FROM hash WHERE path = '/etc/passwd';",
       "interval": 3600
    }

```

If the container is started, let's lookup if your scheduled events are coming to Elastic Security and are visible in Kibana.

###  3.4 - Run adhoc queries via the OSQuery interface

Last part you going to do some local querying.

Connect to the container again.
```
$ docker exec -it es-cluster-osquery-1 bash
```
```
osqueryi
osquery> SELECT name, path, pid FROM processes WHERE on_disk = 0;
osquery> SELECT * FROM process_open_sockets;
```

## Exercise 4 - Add your custom Threat Intelligence

This last part we are going to add our own custom STIX based Threat Intelligence.

This requires us to setup the Custom Threat Intelligence Integration. We are going to deploy this to Linux_Agent_Policy.

Important here is to enable STIX Feeds via files and add `/root/tibundles/*` as input path.

To generate a STIX entry, you can use the example below. Just adjust the date fields to today.

```
{"type":"indicator","spec_version":"2.1","pattern_type":"stix","id":"indicator--329ae6e9-25bd-49e8-89d1-aae4ca52e4a7","created":"2025-05-26T09:12:16.432Z","modified":"2025-05-26T09:12:16.432Z","name":"www.webserver.dynssl.com","description":"www.webserver.dynssl.com resolved to 113.10.246.30, 219.90.112.203, 219.90.112.203, 75.126.95.138, 219.90.112.197, and 202.65.222.45, which overlap with the gwx@123 IP addresses.","pattern":"[domain-name:value = 'www.webserver.dynssl.com' OR ipv4-addr:value = '113.10.246.30' OR ipv4-addr:value = '219.90.112.203' OR ipv4-addr:value = '75.126.95.138' OR ipv4-addr:value = '219.90.112.197' OR ipv4-addr:value = '202.65.222.45']","indicator_types":["malicious-activity","attribution"],"valid_from":"2025-05-26T09:12:16.432678Z"}
```

Again here first install `vim` and save the file to `/tmp`. After that cp the file to `/root/tibundels/tibundle1.txt` and see if you Indicator is being published. You can monitor this using Intelligence under Security.

## Next Steps

You are ready to start with the lab about [Cloud Security](../09-CloudSecurity/README.md) for Elastic Security. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!