# Cluster deployment lab exercises

Welcome to the Cluster Deployment lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about Elastic Security.

The goal is to  get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Virtualization prerequisites
- Operating system preparation
- Podman Installation
- Updating default passwords
- Managing the stack

## Exercise 1 - Validate your containerization prerequisites

This exercise helps you to setup containerization. Most cases you will use a Container Orchestration tool, such as `Kubernetes`. Container workloads are easy to deploy, scale and provide a good way of isolating application services. During the exercises we wil use a Podman (instead of VMWare) setup. Additionally ensure that `Virtualization Technology support` is enabled in the System BIOS.

For Windows users, don't forget to setup Windows Subsystem Layer (WSL2). You can follow the instructions at [Microsoft Learn WSL Setup](https://learn.microsoft.com/en-us/windows/wsl/install-manual).

Also it's good to create a *SymbolicLink* for `docker` to the `podman` executable.

For Windows using PowerShell

```
cd C:\Program files\RedHat\Podman
New-Item -ItemType SymbolicLink -Path "docker.exe" -Target "C:\Program files\RedHat\Podman\podman.exe"
```

### 1 - Setup Podman Desktop

Installation is really straightforward, but be aware of above notes. You may want to download the installer from [Podman.IO]](https://podman.io/). Ensure you have `Docker Compatibility` enabled.  For more installation support read the [Podman Installation Instructions](https://podman.io/docs/installation).

When you join a classroom training, you are lucky, since I've already setup Podman Desktop for you.

### 2.1 - Download Docker Compose Setup files with Git

Now that we have Podman up and running we can start downloading the `Docker Compose Setup` from a GitHub repository called [Elastic-Stack-Docker-Compose](https://github.com/avwsolutions/elastic-stack-docker-compose].

In the previous lab you already have setup a Git client, which you have to use now.

```
git clone https://github.com/avwsolutions/elastic-stack-docker-compose.git
```

For your convenience you can open the `elastic-stack-docker-compose` directory with `VSCode` or your favorite editor. take a look into the `docker-compose.yml` file. This is the actual setup you are going to start.

## Exercise 2.2 - Start Lab Environment using Docker Compose

Now that all setup files are downloaded we can start up our lab environment using `docker compose`.
Ensure that you are in the *root* folder.

```
cd elastic-stack-docker-compose
docker compose up
```

Open a second Terminal and examine if all components are running as expected.

```
docker ps
```

Try to login with your favorite browser (`https://127.0.0.1:5601`) using the credentials below.

Credentials are:
- username: elastic
- password: changeme

*Tip: You can change the default password in the `.env` file*

In short, let's summarize:
- You have installed Podman Desktop.
- You have created an Elastic Stack using a Docker Compose file.

## Exercise 3 - Managing the stack

This last exercise we explain some simple tricks for managing your stack. Think about start and stopping, but also troubleshooting and debugging error logs.

### 5.1 - Stopping and starting environment

Simply remember the following commands. Don't use `docker up / docker down` since that will reset the whole environment to default again.

```
docker compose stop
docker compose start
```

### 5.2 - Troubleshooting

Watch out with docker-compose down, since you have to re-change the password again due reset!

```
docker compose config (check if config is OK)
docker compose ps ( check if all container services are running)
docker compose logs (check logs)
```
## Next Steps

You are ready to start with the next lab about [Advanced Ingestion tools](../03-AdvancedIngestion/README.md) in Elastic Security. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!

