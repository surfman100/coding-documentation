# Microsoft Security

## Defender
aka Microsoft 365 Defender
comprised of:
- Microsoft Defender for Endpoints
- Microsoft Defender for Office 365
- Microsoft Defender for Identity
- Microsoft Defender for Cloud Apps [managed in azure portal](https://portal.azure.com/#view/Microsoft_Azure_Security/SecurityMenuBlade/~/0)
- Microsoft Defender for Cloud workload protections
  - Defender for Servers, App Service, Storage, SQL, OpenSource SQL, KeyVault, Resource Manageer, DNS, Containers, Additional protections

Policies
- File
- Activity
- App Discovery
- Access
- Session
- OAuth App

## Defender for Endpoints
- Attack surface reduction

## Defender for Cloud Apps

## Sentinel
In its simplest form, a SIEM system allows you to:
- Collect and query logs.
  - Use Data Connectors to Azure Activity etc
- Do some form of correlation or anomaly detection.
- Create alerts and incidents based on your findings.
Functionality
- Log Management
- Alerting
- Visualisation
- Incident Management
- Query Data

Features
- Workbooks -> ie a dashboard
- Notebooks
- Watchlist
- Automation
  - Automation rule
  - Playbook with incident/alert/entity trigger
- Analytics -> create queries or incident creation rules. NRT & Schedule can see rule logic

![image](https://github.com/user-attachments/assets/f3fb8a40-88c9-465f-ace4-1c47cdc9454b)

Collecting SysLog and CEF
- install Azure Monitor Agent on the VM source or the log forwarder (linux VM)
- under DataConnectors, create a new rule -> script generated
- script uses rsyslog or syslog-ng, post 514 and Python



## EntraID Protection
Risk Users, Risky sign-in, Risky Apps
Identity based risks. Can feed Conditional Access & SIEM

## Others
Additional integrations to:
- Microsoft Defender for Cloud
- Microsoft Information Protection
