# Introduction lab exercises

Welcome to the Cloud Security lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about Elastic Security.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Run scans with Trivy

## Exercise 1 - Run scans with Trivy

This exercise is to get familiar with Trivy. We will do some simple scanning of the container filesystem and look if we find any vulnerabilities, secrets or misconfigurations.

First download trivy as container using docker.
```
docker run aquasec/trivy
```

- Download trivy as mentioned above.
- Examine the '--help' output.
- You can also run `docker run aquasec/trivy --version`.

Now let's run the filesystem scan. This can be easily done using that container.

- Execute the scan `docker run aquasec/trivy filesystem /`.
- Examine the scan output.

You can also scan a container image.

- Execute the scan `docker run aquasec/trivy image nginx:latest`.
- Examine the scan output.

## Next Steps

You are ready to start with the lab about [EDR Elastic Defend](../10-EDRDefend/README.md) for Elastic Security. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!