# Introduction lab exercises

Welcome to the Advanced Alerting lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about Elastic Security.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Add a simple connector for demo purposes
- Create a case by using a case template
- Create a maintenance window
- Add a advanced connector for API connectivity
- Run an adhoc report

## Exercise 1 - Add a simple connector for demo purposes

This first exercise you are going to work add a simple connector.  The following requirements must be met.

- Notification must be written to the server log.
- Connector must be named triage.
- Action severity is info.
- Action message "You have another TRIAGE!" 

Add this action to your calc.exe detection rule.

- Go to Alerts & Insights under Stack Management
- Click connectors
- Create connector
- Select `server log`
- Name it triage
- Click save

Don't forget to add this to your calc.exe detection rule under actions and use the action message above.
- Trigger calc.exe
- Examine the output. Do you spot logs in 

You can use the following command.

```
docker logs es-cluster-kibana-1 | Select-String TRIAGE
```

You wil see the following line popup after an alert is created.

```
[2025-06-04T18:04:02.693+00:00][INFO ][plugins.actions.server-log] Server log: You have another TRIAGE!
```

## Exercise 2 - Create a case by using a case template

Most organizations is a good practice to work with case templates. In Elastic we can also create them.  Let's give them a try.

First we have to create a `case template` with the following requirements.

- Go to Alerts & Insights under Stack Management
- Click cases
- Click Settings
- Click add template
- Name the template SOC
- Add some useful tags like SOC, EDR, fun for both template and case.
- Add yourself as assignee.
- Keep everything else default.

Now open the calc.exe detection rule again and add an `action` to create a case based on the SOC template, you just created. Ensure that *group_by* is selected on `host.name`.

## Exercise 3 - Create a maintenance window

Maintenance happens and can generate False-positives. To ensure we minimise this we can create a maintenance window.

- Go to Alerts & Insights under Stack Management
- Click Maintenance Windows
- Create Window
- Name it 'Weekly Reboot'.
- Add you weekly schedule, every tuesday from 20:00 til 21:00
- You can add a filter to exclude alerts like using the `kibana.alert.rule.uuid` .

## Exercise 4 - Add a advanced connector for API connectivity

Most enterprises use ticketing systems, which connect over REST APIs. For this you can use the Webhook connector. Let's configure a mockup webhook.

The following requirements must be met.

- Notification must be written to a webhook.
- Connector must be named Fake REST API.
- POST must go to endpoint: https://jsonplaceholder.typicode.com/posts
- Add no authentication.
- Add a HTTP header `Content-type: application/json; charset=UTF-8`
- Action severity is critical.
- Action message must contain alert variables.

Add this action to your calc.exe detection rule.

- Go to Alerts & Insights under Stack Management
- Click connectors
- Create connector
- Select Webhook connector
- Name it 'Fake REST API'
- Click Save

Use the test option (see Test tab) to validate if the connectivity is setup correctly.
Use the following body.

```
{
    "title": "Hello notify",
    "body": "Hello training",
    "userid": 100 
}
```

- Examine the test results? Did they go well?

Don't forget to add this to your calc.exe detection rule under actions and write a more dynamic message using  variables. You can use most *alert* and *context* variables, see top-right.

- Trigger calc.exe to validate the action.

## Exercise 5 - Create an adhoc report

Still reports can be helpful. This feature is there since the beginning. Let's save the [Elastic Agent] Overview dashboard to PDF and share this with your colleagues.

- Open Dashboards, under Analytics
- Search for Elastic Agent
- Choose the Overview dashboard
- On the right-top click Share
- Click Export and PDF.
- Export file
- Go to  Stack Management > Reporting to see and download the report.

A popop will be shown to download the report. Examine the report. Also tryout the PNG option.

## Next Steps

You are ready to start with the lab about [Dashboards](../07-Dashboards/README.md) for Elastic Security. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!