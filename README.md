# ITProfessorCloud Logic Apps

> **Practical, production-ready Microsoft Sentinel playbooks by [ITProfessor.cloud](https://itprofessor.cloud)**

This repo contains Logic App Consumption playbooks built for real-world Microsoft Sentinel deployments. Every playbook follows the official Microsoft Sentinel ARM pattern - one-click Deploy to Azure, MSI where supported, no hardcoded environment values.

---

## Playbooks

| Playbook | Description | Deploy |
|---|---|---|
| [Incident-Send-Email](./Incident-Send-Email) | Sends an HTML-formatted email on new Sentinel incident creation | [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FITProfessorCloud%2FLogicApps%2Fmain%2FIncident-Send-Email%2Fazuredeploy.json) |
| [Sentinel-Nag-Machine](./Sentinel-Nag-Machine) | Nags your team in Teams every 15 mins about unowned Sentinel incidents - friendly nudge under 1hr, increasingly angry after 2hrs, with one-click ownership assignment | [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FITProfessorCloud%2FLogicApps%2Fmain%2FSentinel-Nag-Machine%2Fazuredeploy.json) |
