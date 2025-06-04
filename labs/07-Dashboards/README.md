# Introduction lab exercises

Welcome to the Dashboard lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about Elastic Security.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Explore default dashboards
- Create a custom dashboard
- Export dashboard objects
- Add a Runtime field

## Exercise 1 - Explore default dashboards

This first exercise is about exploring the default dashboards that are shipped with Elastic Security. Take special attention to the *Data Quality dashboard*, since this a good example how dashboards become more *interactive*.

- Open Dashboards, under Security
- Give every dashboard a try. Examine the visualizations and think about when they can become useful.
- For the *Data Quality dashboard* try the interactive feature `Check All`.

## Exercise 2 - Create a custom dashboard

Sometimes you need a custom dashboard. You know what you want, you only need Lens to create some great looking visualizations. Don't forget to add two controls for selecting the date range and filtering on `host.name`.

- Open Dashboards, under Security
- Click Create dashboard.
- Add a first visualization using Lens. For example a Terms or histogram for 'Process Usage`. Don't forget to save this visualization. Give it a self-explainable name and description.
- Add two controls to manipulate the 'Time Interval' and 'hostname' selection.
- Save you dashboard and verify it's available under Security.

## Exercise 3 - Export dashboard objects

Sometimes it's good to export dashboards. This can be easily done using single export or using `Saved Objects` export feature. You are going to export all dashboards for backup purposes.

- Open Stack management
- Open Saved Objects under Kibana
- Filter the dashboards, don't forget to select all
- Click on Export , top-right.

Now examine the exported JSON files and look how they are formatted. Do you recognise your own custom dashboard?

## Exercise 4 - Add a Runtime field

Do you know `Scripted Fields`. They are replaced by a better performing solution called `Runtime Fields`.

You can add them by adding them to a component template, under mappings, like extending `logs@custom`. You may also extend another `@custom` that minimizes the impact for only 'Windows PowerShell Operational' logs. Then you create `logs-windows.powershell_operational@custom`.

- First add the object called `course`. This wil be the placeholder.
- Create a runtime field called course.system_id as type KEYWORD
- Add the *Painless* script below.

```
String systemId = "CI_" + doc['host.name'].value.toUpperCase() + "_X001";
if (systemId != null) emit(systemId);
```

Ensure that you did a rollover to activate the runtime field. Take notice that `logs@custom` impacts all data streams that start with 'log-*'. 

If you chose 'Windows PowerShell Operational' logs, then the datastream is called `logs-windows.powershell_operational-default`.

Below the steps to activate.

- Open Dev Tools
- POST <datastream>/_rollover

## Next Steps

You are ready to start with the lab about [Advanced Investigation](../08-AdvancedInvestigation/README.md) for Elastic Security. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!