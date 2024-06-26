### S0154 - Cobalt Strike: NamedPipe

#### DESCRIPTION

Cobalt Strike is a famous Pen Test tool that is used by pen testers as well as attackers alike to compromise an environment.
CobaltStrike uses named pipes for communication between processes. Default beacon configs use pipes in the format "MSSE-x-server", where "x" is a number from 1 to 4 characters.

**Example:**

> "MSSE-x-server", where "x" is a number from 1 to 4 characters

**Related**

CobaltStrike

**Reference:**

https://github.com/SigmaHQ/sigma/blob/dcfb4c5c28431dcdc1d26ed4e008945965afd8ed/rules/windows/pipe_created/pipe_created_mal_cobaltstrike.yml#L4 <br>
https://twitter.com/d4rksystem/status/1357010969264873472 <br>
https://labs.f-secure.com/blog/detecting-cobalt-strike-default-modules-via-named-pipe-analysis <br>
https://github.com/SigmaHQ/sigma/issues/253 <br>
https://blog.cobaltstrike.com/2021/02/09/learn-pipe-fitting-for-all-of-your-offense-projects <br>
https://redcanary.com/threat-detection-report/threats/cobalt-strike <br>
https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/Microsoft%20365%20Defender/Command%20and%20Control/C2-NamedPipe.yaml <br>

#### ATT&CK TACTICS

{{mitre("S0154")}}

Data Source(s): [Named Pipe](https://attack.mitre.org/datasources/DS0023)

#### SENTINEL RULE QUERY

```
let selection_MSSE = dynamic([@'\MSSE-', '-server']);
let selection_Pipename = dynamic(['\\postex_', '\\status_', '\\msagent_', '\\mojo_', '\\interprocess_', '\\samr_', '\\netlogon_', '\\srvsvc_', '\\lsarpc_', '\\wkssvc_']); // Also include the pipe "\postex_ssh_"
DeviceEvents
| where ActionType == "NamedPipeEvent"
| extend FileOperation_ = tostring(AdditionalFields.FileOperation)
| extend PipeName_ = tostring(AdditionalFields.PipeName)
| where FileOperation_ == "File created"
| where PipeName_ has_all (selection_MSSE) or PipeName_ has_any (selection_Pipename)
| where not(InitiatingProcessFolderPath contains "kdsstm.exe" and PipeName_ contains "kyoceradocumentsolutions") // Kyocera drivers
//| summarize count(), earliest_Timestamp=min(TimeGenerated) by ActionType, DeviceName, InitiatingProcessParentFileName, InitiatingProcessAccountDomain, InitiatingProcessAccountName, InitiatingProcessFolderPath, InitiatingProcessCommandLine, FileOperation_, PipeName_, TenantId
```

#### Triage

1. Remove the comment "//" in 'summarize' statement in above KQL to assist in analysis and removing data duplicates.
1. Inspect named pipe pattern if matching "MSSE-x-server"
1. Examine the InitiatingProcessFolderPath folder location, and check for any mistype on service name

#### VERSION

Version 2.1 (date: 08/11/2023)
