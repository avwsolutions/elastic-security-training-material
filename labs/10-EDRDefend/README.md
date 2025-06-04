# Introduction lab exercises

Welcome to the EDR Elastic Defend lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about Elastic Security.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Enable integration with Configuation Preset
- Creating a event filter for Excluding events
- Creating a host isolation exception
- Validate Malware Protection data sync is enabled


## Exercise 1 - Enable integration with Configuation Preset

First we are going to enable Elastic Defend.

### 1.1 - Now ensure Elastic Defend integration is activated for the Windows-Agent-Policy

- Open Fleet under Management. Fleet Central Management is opened. 
- On tab Agent Policies, click the Windows-Agent-Policy.
- Click Add integration.
- Search for Elastic Defend.
- Click Add Elastic Defend.
- Examine the Configuration Settings that are available.
- Choose Traditional Endpoints and select 'Data Collection'.
- Save and deploy changes.

## Exercise 2 - Creating a event filter for Excluding events

Some situations you don't want certain events. Here we are going to stop logging events from `tracee.exe`, which polutes your Elasticsearch indices.

First let's prepare such. Just copy notepad.exe to C:\elastic\tracee.exe like `Creating a event filter for Excluding events`. Validate if `tracee.exe` is catched.

Now let's stop these events by creating an event filter.

- Open Manage, under Security.
- Open Event filters.
- Click Add event filter.
- Give it a name like Exclude tracee.exe
- Add a condition named `process.name is tracee.exe`
- Keep other default.
- Add event filter.

They are still coming in? Why . You maybe are looking to Windows integration events, so take notice of this.

You may want to create a `trusted application` and `block list` yourself? Found can find them under Manage (under Security). For example add `tracee.exe` to an block list. 

Are they currently blocked ? Explain what you observe. 


## Exercise 3 - Creating a host isolation exception

With Elastic Defend we can put a host in isolation. This is great, but sometimes other Security tools must be connected. For this reason you can add these exceptions. For example we use Ghost as malware analysis tool.

Let's add the exception.

- Open Manage, under Security.
- Open Host Isolation Exceptions.
- Click Add host isolation exception.
- Give it a name like Ghost malware analysis.
- Optional description like Can access my sandbox Labs (10.120.5.0/24), even when isolated.
- Add the IP Address or CIDR as condition. `10.120.5.0/24`
- Keep other default.
- Add host isolation exception.


## Exercise 4 - Integrate with Microsoft Defender

### 4.1 - Validate Malware Protection data sync is enabled 

This last exercise we are going to validate if we have configured the integration with Microsoft Defender. To ensure that they are integrated you have to enable the sync with malware protection level.

- Open Manage, under Security.
- Open Policies.
- Click the newly created elastic_defend1 policy.
- Scroll to the bottom at the Policy settings tab.
- Choose the Sync with malware protection level ratio
- Click save.

Now you have integrated both Elastic Defend with Microsoft Defender.

### 4.2 - Exclude Defender from Elastic Defend

Some scenarios Elastic Defend wil identify or scan Microsoft Defender. It's a good practice to add this as Trusted Application, so performance is not getting degraded. This visa versa.

Now let's stop this engine to be scanned by creating an trusted application.

- Open Manage, under Security.
- Open Trusted applications.
- Click Add trusted applicaton.
- Give it a name like Exclude MS Defender
- Add a condition `Signer name is Microsoft Windows Publisher` and `directory is C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.25040.2-0\MpDefenderCoreService.exe`.
- Keep other default.
- Add trusted application.

## Next Steps

You are ready to start with the lab about [Advanced Entity Analytics](../11-AdvancedAnalytics/README.md) for Elastic Security. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!