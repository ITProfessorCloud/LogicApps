# Incident Send Email

> **Playbook by [ITProfessor.cloud](https://itprofessor.cloud)**

A Microsoft Sentinel Logic App playbook that fires an HTML-formatted email notification every time a new incident is created. Attach it to a Sentinel automation rule scoped to **"When incident is created"**

---

## What it does

- Triggers on the Microsoft Sentinel **incident-creation** webhook
- Composes a clean HTML email with incident title, severity, status, created time, description and a direct link to the Sentinel portal
- Sends the email via Office 365
- Uses **System Assigned Managed Identity** for the Sentinel connection - no credential management needed

---

## Deploy

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FITProfessorCloud%2FLogicApps%2Fmain%2FIncident-Send-Email%2Fazuredeploy.json)

---

## Parameters

| Parameter | Description | Default |
|---|---|---|
| `PlaybookName` | Name of the Logic App resource | `Incident_Send_Email` |
| `NotificationEmail` | Email address to receive incident alerts | *(required)* |

---

## Post-deployment steps

1. **Authorize Office 365 connection** - go to the deployed Logic App > API connections > `Office365-<PlaybookName>` > Edit API connection > Authorize
2. **Grant Log Analytics Reader** - assign the Logic App's managed identity the **Log Analytics Reader** role on the Log Analytics Workspace
3. **Enable the Logic App** - it deploys in Disabled state, enable it once the Office 365 connection is authorized
4. **Attach to automation rule** - in Microsoft Sentinel > Automation > Create rule > trigger: *When incident is created* > action: *Run playbook* > select this playbook

---

## Resources created

| Resource | Type |
|---|---|
| `Incident_Send_Email` | Microsoft.Logic/workflows |
| `MicrosoftSentinel-<PlaybookName>` | Microsoft.Web/connections |
| `Office365-<PlaybookName>` | Microsoft.Web/connections |

---

*Part of the [ITProfessorCloud/LogicApps](https://github.com/ITProfessorCloud/LogicApps) collection - practical, production-ready Sentinel playbooks.*
