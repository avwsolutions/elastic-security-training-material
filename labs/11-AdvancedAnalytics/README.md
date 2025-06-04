# Introduction lab exercises

Welcome to the Cloud Security lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about Elastic Security.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Enable Entity and run a preview
- Enable Entity store

## Exercise 1 - Enable Entity and run a preview

This exercise is to get familiar with Entity Analytics. First we will enable the `Entity Risk Score` engine.
After that we are going to preview our `calc.exe` proces.

### 1.1 - Enable the Entity Risk score engine

Now let's start this engine calculating risk scores for entities.

- Open Manage, under Security.
- Open Entity Risk Score.
- Enable the Entity Risk Score engine.
- Save if needed.

## 1.2 - Run a preview for calc.exe

Now lookup the level and score for the process.name calc.exe.

- Open Manage, under Security.
- Open Entity Risk Score.
- Type at right, Preview pane the `process.name:"calc.exe" ` 
- Lookup wat the score means. 
- Exam why the level is set to unknown. Try to play around with the time filter. Also look if the criticality has been set.

## Exercise 2 - Enable Entity store

Sometimes manual intervention or administration is needed. To achieve this a Entity Store exists.  First we will enable the `Entity Store` engine.

After that we are going to preview our `calc.exe` proces.
### 1.1 - Enable the Entity Store engine

Now let's start this engine calculating risk scores for entities.

- Open Manage, under Security.
- Open Entity Store.
- Enable the Entity Store engine.
- Save if needed.

## 2.2 - Register your entities

Now register the asset criticality of your entities like user.name and host.name.

- Prepare an TXT input file with notepad.

```
user,<your username>,low_impact
host,<your host>,extreme_impact
```
- Open Manage, under Security.
- Open Entity Store.
- Drag your txt file to the drop area or upload with select file.
- When correctly formatted you can Assign them.


Now repeat exercise 1.2. What differences do you see?

## Next Steps

You are ready to start with the lab about [EDR Elastic Defend](../10-EDRDefend/README.md) for Elastic Security. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!