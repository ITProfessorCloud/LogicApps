# Sentinel Nag Machine

> **Playbook by [ITProfessor.cloud](https://itprofessor.cloud)**

A Microsoft Sentinel Logic App playbook that runs every 15 minutes and nags your team in Microsoft Teams about unowned incidents. Sends an Adaptive Card for incidents under 1 hour old, and an increasingly angry card for incidents 2+ hours old - with one-click ownership assignment back to Sentinel.

---

## What it does

- Runs on a 15-minute recurrence trigger
- Queries Log Analytics for all **New** Sentinel incidents with no owner
- For incidents **less than 1 hour old** - posts a friendly nudge Adaptive Card to Teams
- For incidents **2+ hours old** - posts an escalating, angry Adaptive Card to Teams
- Responder can **Take Ownership** or **Dismiss** directly from the Teams card
- If ownership is taken, the Logic App calls back to Sentinel and assigns the incident to that user and sets status to **Active**
- Uses **System Assigned Managed Identity** for the Sentinel connection - no credential management needed

---

## Deploy

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FITProfessorCloud%2FLogicApps%2Fmain%2FSentinel-Nag-Machine%2Fazuredeploy.json)

---

## Parameters

| Parameter | Description | Default |
|---|---|---|
| `PlaybookName` | Name of the Logic App resource | `Sentinel-Nag-Machine` |

---

## Post-deployment steps

1. **Authorize the Azure Monitor Logs connection** - open the connection resource in the portal and authenticate with an account that has access to your Log Analytics Workspace
2. **Authorize the Teams connection** - open the Teams connection resource and sign in with the account the Flow bot will post as
3. **Set Teams Group ID and Channel ID** - edit the Logic App and populate the `groupId` and `channelId` fields in both Adaptive Card actions with your target Teams channel
4. **Grant Sentinel Responder role** - assign the Logic App's managed identity the **Microsoft Sentinel Responder** role on the Log Analytics Workspace so it can update incidents
5. **Enable the Logic App** - it deploys in Disabled state; enable it once all connections are authorized

---

## Resources created

| Resource | Type |
|---|---|
| `Sentinel-Nag-Machine` | Microsoft.Logic/workflows |
| `AzureMonitorLogs-<PlaybookName>` | Microsoft.Web/connections |
| `Teams-<PlaybookName>` | Microsoft.Web/connections |
| `MicrosoftSentinel-<PlaybookName>` | Microsoft.Web/connections |

---

## Blog post

Full write-up and walkthrough: [The Nag Machine - A Logic App that badgers your team about unowned Sentinel incidents](https://www.itprofessor.cloud/the-nag-machine-a-logic-app-that-badgers-your-team-about-unowned-sentinel-incidents/)
