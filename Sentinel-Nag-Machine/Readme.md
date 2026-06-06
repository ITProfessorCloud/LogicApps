# Sentinel Nag Machine

> **Playbook by [ITProfessor.cloud](https://itprofessor.cloud)**

A Microsoft Sentinel Logic App playbook that runs on a recurring schedule, queries for unowned incidents, and sends Teams adaptive cards to your SOC channel badgering analysts to take ownership. Escalating message urgency based on incident age.

## What it does

- Runs every 15 minutes via a recurrence trigger
- Queries Log Analytics for Sentinel incidents in **New** status with no owner that are older than 30 minutes
- For incidents under 1 hour old, sends a friendly nudge via Teams adaptive card
- For incidents 2 or more hours old, sends an escalated urgent Teams adaptive card
- Analysts can respond directly in Teams to **Take Ownership** or **Dismiss** the incident
- On ownership selection, automatically assigns the incident to the responder and sets status to **Active** via the Microsoft Sentinel API
- Uses **System Assigned Managed Identity** for the Sentinel connection. No credential management needed

## Deploy

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FITProfessorCloud%2FLogicApps%2Fmain%2FSentinel-Nag-Machine%2Fazuredeploy.json)

## Parameters

| Parameter | Description | Default |
|---|---|---|
| `PlaybookName` | Name of the Logic App resource | `Sentinel-Nag-Machine` |

## Post-deployment steps

1. **Authorise the Teams connection** - open the Teams API connection in the portal and authorise it with an account that has access to your SOC Teams channel
2. **Configure the Azure Monitor Logs connection** - authorise it and point it at your Log Analytics Workspace
3. **Set your Teams channel** - update the `groupId` and `channelId` values in both adaptive card actions to target your SOC channel
4. **Grant Microsoft Sentinel Responder** - assign the Logic App managed identity the **Microsoft Sentinel Responder** role on your Sentinel workspace so it can update incidents
5. **Enable the Logic App** - it deploys in Disabled state, enable it once all connections are authorised

## Resources created

| Resource | Type |
|---|---|
| `Sentinel-Nag-Machine` | Microsoft.Logic/workflows |
| `AzureMonitorLogs-<PlaybookName>` | Microsoft.Web/connections |
| `Teams-<PlaybookName>` | Microsoft.Web/connections |
| `MicrosoftSentinel-<PlaybookName>` | Microsoft.Web/connections |

*Part of the [ITProfessorCloud/LogicApps](https://github.com/ITProfessorCloud/LogicApps) collection. Practical, production-ready Sentinel playbooks.*
