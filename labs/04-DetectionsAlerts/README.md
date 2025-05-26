# Introduction lab exercises

Welcome to the Elastic Stack as Detection & Alerts lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about Elastic Security.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Import pre-built rules
- Duplicate pre-built rule for customization
- Create a Custom Query detection-rule

## Exercise 1 - Import pre-built rules

This first exercise you are going to import the pre-built detection-rules. 

You can do this by the following steps.

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

You are ready to start with the lab about [Advanced Querying](-./05-AdvancedQuerying/README.md) for Elastic Security. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!