# Introduction lab exercises

Welcome to the Introduction lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about Elastic Security.

The goal is to  get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Training resources
- Training setup
- Lab deployment
- Manage the Stack

## Exercise 1 - Downloading training resources

This first exercise you are required to download the training resources. You need to download two packages.

- elastic-security-training-material
- elastic-stack-docker-compose

Most simply way is using Curl or [Download the ZIP](https://github.com/avwsolutions/elastic-security-training-material/archive/refs/heads/main.zip) using your favorite browser. Git is not part of this course, but we encourage using the Git client, which you can [download](https://git-scm.com/downloads/guis) for free.

Either choose one of the options to download the training material.

### 1.1 - Download using Curl

First the lab material and second the Second the deployment code.

```
cd
curl -L https://github.com/avwsolutions/elastic-security-training-material/archive/refs/heads/main.zip -o elastic-security-training-material.zip
unzip elastic-security-training-material-main.zip
mv elastic-security-training-material-main elastic-security-training-material

cd
curl -L https://github.com/avwsolutions/elastic-stack-docker-compose/archive/refs/heads/main.zip -o elastic-stack-docker-compose.zip
unzip elastic-stack-docker-compose-main.zip
mv elastic-stack-docker-compose-main elastic-stack-docker-compose
```

### 1.2 - Download using Git

```
cd
git clone https://github.com/avwsolutions/elastic-security-training-material.git
git clone https://github.com/avwsolutions/elastic-stack-docker-compose.git
```

If you want to know more about Git, the Version Control System just visit the [Git-SCM Website](https://git-scm.com/).

Now that you have downloaded the material (and extracted the ZIP file) you may want to look into this directory.

```
cd ~/elastic-security-training-material
ls
```
## Exercise 2 - Deploying the training setup

This exercise you will read through training setup for Elastic Security and understand the components we will use. Important to understand that Elastic Stack is built by two core components called `ElasticSearch` and `Kibana`.Nowadays we cannot deploy an Elastic Stack without `Fleet Server` and `Elastic Agents`. Data itself is still stored as `JSON` documents. The `ElasticSearch Indices` are based on the `NoSQL` concept, so from the early days you don't require a schema to start ingesting data. For `Elastic Solutions` like `Elastic Security` it's mandatory to adopt the `Elastic Common Schema`, which helps to standardize `Dashboards`, `Queries`and other resources which is part of an `Elastic Integration`. As you see we wil also briefly touch integrations for `OSQuery Logs`, `Zeek`, `Windows` and some more. Almost everything became an Integration, just like their `EDR`solution called `Elastic Defend`. Additionally we will introduce `Beats` and the `Logstash Agent` to load additional `data sets`, next to the `sample data sets` we primarily integrate using the `Elastic Agent`.

<img src="https://github.com/avwsolutions/elastic-security-training-material/blob/main/labs/01-introduction/content/training-setup.png?raw=true" alt="training-setup">

### 2.2 - Examine the training deployment files

Examine the recently downloaded training deployment files. They are stored under the `elastic-stack-docker-compose` folder.
- Review the downloaded training resources () and give extra attention to the `docker-compose.yml`.
- Can you find the core components that built Elastic Stack?

### 2.3 - Start Lab Environment using Docker Compose

Now that all  files are downloaded we can start up our lab environment using `docker compose`.
Ensure that you are in the *root* folder.

```
cd elastic-stack-docker-compose
docker compose up -d
```
Examine if all contiainers are running as expected. They should have a *healthy* state.

```
docker ps
```

### 2.4 - First login in the Elastic Security Lab environment

Try to login with your favorite browser (`https://127.0.0.1:5601`) using the credentials below.

Credentials are:
- username: elastic
- password: changeme

*Tip: You can change the default password in the `.env` file*

In short, let's summarize:
- You have installed Podman Desktop.
- You have created an Elastic Stack using a Docker Compose file.
- You validated the availability by log into the Kibana console.

## Exercise 3 - Managing the stack

This last exercise we explain some simple tricks for managing your stack. Think about start and stopping, but also troubleshooting and debugging error logs.

### 3.1 - Stopping and starting environment

Simply remember the following commands. Don't use `docker up / docker down` since that will reset the whole environment to default again.

```
docker compose stop
docker compose start
```

### 3.2 - Troubleshooting

Watch out with docker-compose down, since you have to re-change the password again due reset!

```
docker compose config (check if config is OK)
docker compose ps ( check if all container services are running)
docker compose logs (check logs)
```

## Next Steps

You are ready to start with the second lab about [Elastic Stack as Fundament](../02-stackfoundation/README.md) for Elastic Security. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!