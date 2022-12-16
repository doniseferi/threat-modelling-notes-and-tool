# Threat Modelling Session with Microsoft

## The CIA Security Trident Distilled

<p align="center" background-color="white">
<img src="./cia_triad.png?sanitize=true" width="250px" />
</p>

The CIA trident, confidentiality, integrity and availability are the three pillars of security. _For any resource to be considered secure it must consider and address all sides of the CIA trident._

- Confidentiality is a systems ability to ensure correct access control over data.
- Integrity is a systems ability to ensure data validity.
- Availability is the system's ability to remain running and ensure it is available.

## Confidentiality

For any system to maintain confidentiality it must ensure its data is private and enforce correct access control. Data confidentiality can be ensured by:
- Data classification and labelling
- Strong and <b>correct</b> access control.
- Strong authentication methods.
- Encryption of data in process, transit and storage.
- Stenography
- Training for all individuals with access to data

Some common confidentiality failures are:
- Broken access control.
- Cryptographic failures.
- Security misconfiguration.
- Escalation of privileges.
- Unauthorized access to data.
- Unprotected passwords.
- <b>Human error</b>

## Integrity

For any system to maintain its integrity it must provide certainty that information is uncompromised during or after transmission. Systems must protect data from unauthorized access, modification and deletion. Data integrity can be ensured by:
- Encryption of data at rest and in transit.
- Enforce strong password.
  - Hash and salt passwords.
- Identify and perform risk based analysis on resources and partition accordingly.

Some common integrity failures are:
- Failure in CI/CD pipelines.
  - If a bad actor gains access over CI/CD pipelines then malicious software will propagate from a trusted source.
- Update compromise from a trusted or central source.
- Compromised open-source code.

## Availability

For any system to remain useful it must above all remain available. Organisations that require highly-available resources solve this problem with architectures that are specifically designed to improve availability. Some of those patterns are:
- Functional decomposition
  - unlocks horizontal scaling
- Asynchronous architectural patterns
  - unlocks the ability to build resilient systems
- Geographic redundancy
- Caching
- Various other methods

The main threats that effecting system availability are:
- Bad actors
  - DDoS.
- Human error (Architectural)
  - Failing to acknowledging the possibility of failure is stripping your ability to react and handle the inevitable failures that certainly will arise.
  - Self DoS
- Infrastructural
- Data inconsistency and poor data
  - LSK - (precondition's cannot be strengthen, postcondition's cannot be weakened, invariance must be preserved)

## ALCOA+ principles of data integrity

Alcoa+ is an acronym for the principles defined for best practices and methodologies for healthy data management. Detailed as following:

Attributable: Do you know how data is created or obtained, and by whom?
Legible: Can you read and understand the data and the records are permanent
Contemporaneous: Do you know how data appeared in its initial state and what happened to it throughout the different stages of its lifecycle?
Original: Can you identify the data source and maintain the data's original state?
Accurate: Is data errorless and does it conform to the protocols of the applications for which it is used.
Complete: Is all the data available?
Consistent: Does the data meet consistency requirements? Ordering, chronology maintained etc?
Enduring: Is the data stored securely for long term use?
Available: Is the data accessible on demand?   

___

<br />

# The STRIDE model
_Courtesy of owsap.org_
## Spoofing Threats

| Threat Examples                        | Attacker Action                       | Notes                                               |
| -------------------------------------- | -------------------------------------------- | --------------------------------------------------- |
| Spoofing a process on the same machine | Creates a file before the real process       |                                                     |
|                                        | Renaming/linking                             | Replacing a well-known process with a malicious     |
|                                        |                                              | process with the same name                          |
|                                        | Renaming                                     | Naming your process something “legitimatesounding”  |
| Spoofing a File                        | Creates a file in a local directory          |                                                     |
|                                        | Creates a link and changes it                | Change should happen between check and access       |
|                                        | Creates many files in the expected directory | Useful for spoofing .pid or .lock files             |
| Spoofing a Machine                     | ARP Spoofing                                 |                                                     |
|                                        | IP Spoofing                                  |                                                     |
|                                        | DNS Spoofing                                 | Forward or reverse                                  |
|                                        | DNS Compromise                               | Compromise TLD, registrar, or DNS operator          |
|                                        | IP Redirection                               | Switch/Router level                                 |
| Spoofing a Person                      | Sets e-mail display name                     |                                                     |
|                                        | Takes over a real account                    |                                                     |
| Spoofing a Role                        | Declares themselves to be that role          | Opening a special                                   |
|                                        |                                              | account with a relevant name                        |
|                                        |                                              | Asserting role through request/profile manipulation |

___

<br />
<br />

## Tampering Threats

| Threat Examples          | Attacker Action                          | Notes                                                                             |
| ------------------------ | ----------------------------------------------- | --------------------------------------------------------------------------------- |
| Tampering with a File    | Modifies a file they own, and on which you rely |                                                                                   |
|                          | Modifies a file you own                         |                                                                                   |
|                          | Modifies a file on a file server that you own   | Processes can include files from remote domains                                   |
|                          | Modifies a file on their file server            | XML frequently includes remote schema refs                                        |
|                          | Modifies links or redirects                     |                                                                                   |
| Tampering with Memory    | Modifies your code                              | Hard to defend against when the attacker is already running code as the same user |
|                          | Modifies data supplied to your API              | Pass by value, never by reference, when crossing a trust boundary                 |
| Tampering with a Network | Redirects data flow to their machine            | Often first stage of Tampering                                                    |
|                          | Modifies data flowing over a network            | Even easier when wireless networks are involved                                   |

___

<br />
<br />

# Repudiation Threats 

| Example               | Attacker Action                                                                         | Notes                                               |
| --------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------- |
| Repudiating an Action | Claims not to have clicked                                                              |
|                       | Claims not to have received                                                             | How do we “prove” receipt?                          |
|                       | Claims to have been a fraud victim                                                      |                                                     |
|                       | Uses someone else’s account                                                             |                                                     |
|                       | Uses someone else’s payment instrument                                                  |                                                     |
| Attacking the Logs    | Notices you have no logs                                                                |                                                     |
|                       | Puts attacks in the logs to confuse logs, logreading code, or a person reading the logs | Corrupting the logs can invalidate them as evidence |

___

# Information Disclosure Threats

| Example                                    | Attacker Action                                      | Notes                     |
| ------------------------------------------ | ---------------------------------------------------- | ------------------------- |
| Information Disclosure against a Process   | Extracts secrets from error messages                 |                           |
|                                            | Extracts machine secrets from error cases            | Can make ASLR less useful |
|                                            | Extracts business/ personal secrets from error cases |                           |
| Information Disclosure against Data Stores | Takes advantage of inappropriate or missing          |                           |
|                                            | ACLs                                                 |                           |
|                                            | Takes advantage of bad database permissions          |                           |
|                                            | Finds file protected by obscurity                    |

___

<br />
<br />

# Denial of Service Threats

| Example                                | Attacker Action                           | Notes |
| -------------------------------------- | ----------------------------------------- | ----- |
| Denial of Service against a Process    | Absorbs memory                            |       |
|                                        | Absorbs CPU                               |       |
|                                        | Uses process as an amplifier              |       |
| Denial of Service against a Data Store | Fills up data store                       |       |
|                                        | Makes enough requests to slow down system |       |
| Denial of Service against a Data Flow  | Consumes network resources                |       |

___

<br />
<br />

# Elevation of Privilege Threats 

| Example                                                            | Attacker Action                                                                               | Notes                                                       |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| Elevation of Privilege against a Process by Corrupting the Process | Sends inputs that the process does not handle properly                                        | Very common, and frequently high-impact                     |
|                                                                    | Gains access to read or write memory inappropriately                                          | Reading memory can enable further attacks                   |
| Elevation through Missed Authorisation        Checks               |                                                                                               |                                                             |
| Elevation through Buggy Authorisation Checks                       |                                                                                               | Centralise checks, to make errors easier to find and manage |
| Elevation through Data Tampering                                   | Modifies bits on disk (or in memory) to do things other than what the authorised user intends |                                                             |

___

## Elements Effected By Stride

| **Element**     | **S** | **T** | **R** | **I** | **D** | **E** |
| --------------- | ----- | ----- | ----- | ----- | ----- | ----- |
| External Entity | **X** |       | **X** |       |       |       |
| Process         | **X** | **X** | **X** | **X** | **X** | **X** |
| Data Flow       |       | **X** |       | **X** | **X** |       |
| Data Store      |       | **X** | **?** | **X** | **X** |       |

___

## OWASP Top 10 (2022)

1. Broken Access Control
2. Cryptographic Failures
3. Injection
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable and Outdated Components
7. Identification and Authentication Failures
8. Software and Data Integrity Failures
9. Security Logging and Monitoring Failures
10. Server-Side Request Forgery (SSRF)

# Thread Modelling Tool

### How to threat model
_Courtesy of synopsys_<br/>
When threat modelling follow the following high level steps:
1. Define the scope and depth of analysis. Determine the scope with stakeholders, then break down the depth of analysis for individual development teams so they can threat model the software.

2. Gain a visual understanding of what you’re threat modeling. Create a diagram of the major system components (e.g., application server, data warehouse, thick client, database) and the interactions among those components.

3. Model the attack possibilities. Identify software assets, security controls, and threat agents and diagram their locations to create a security model of the system (see Figure 1). Once you’ve have modeled the system, you can identify what could go wrong (i.e., the threats) using methods like STRIDE.

4. Identify threats. To produce a list of potential attacks, ask questions such as the following:

                    Are there paths where a threat agent can reach an asset without going through a control?

                    Could a threat agent defeat this security control?

                    What must a threat agent do to defeat this control?

5. Create a traceability matrix of missing or weak security controls. Consider the threat agents and follow their control paths. If you reach the software asset without going through a security control, that’s a potential attack. If you go through a control, consider whether it would halt a threat agent or whether the agent would have methods to bypass it.

## Application

Microsoft have made a threat modelling tool available which has been attached to this repository on [this link](./TMT7.application).

### Running Microsoft's threat modelling tool

Running the application is as simple as double clicking the '[TMT7.application](./TMT7.application)' file attached to this repo. 

#### Create a new threat model

To start threat modelling once you have opened the application ensure the 'Template For New Models' is set to 'Azure Threat Model Template (x.x.x)' and click the big azure coloured 'Create A Model' button. Once you have created your model click the reports tab at the top, then the 'Create Full Report' tab and provide the name and location for the model to be saved.

#### Load an existing threat model

Once you have opened the threat modelling application click the big azure coloured 'Open A Model' button and load an already created model, such as the example one provided [here](./DcrModell.tm7).

_____
# Threat Modeling Report Example

<span tabindex="0">Created on 01/12/2022 15:35:35</span>

**Threat Model Name:**

**Owner:**

**Reviewer:**

**Contributors:**

**Description:**

**Assumptions:**

**External Dependencies:**

### Threat Model Summary:

<table>

<tbody>

<tr tabindex="0" role="row">

<td>Not Started</td>

<td>37</td>

</tr>

<tr tabindex="0" role="row">

<td>Not Applicable</td>

<td>0</td>

</tr>

<tr tabindex="0" role="row">

<td>Needs Investigation</td>

<td>0</td>

</tr>

<tr tabindex="0" role="row">

<td>Mitigation Implemented</td>

<td>0</td>

</tr>

<tr tabindex="0" role="row">

<td>Total</td>

<td>37</td>

</tr>

<tr tabindex="0" role="row">

<td>Total Migrated</td>

<td>0</td>

</tr>

</tbody>

</table>

* * *

## Diagram: Diagram 1

![Diagram 1 diagram screenshot
            ](data:image/png;base64,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)

### Diagram 1 Diagram Summary:

<table>

<tbody>

<tr tabindex="0" role="row">

<td>Not Started</td>

<td>37</td>

</tr>

<tr tabindex="0" role="row">

<td>Not Applicable</td>

<td>0</td>

</tr>

<tr tabindex="0" role="row">

<td>Needs Investigation</td>

<td>0</td>

</tr>

<tr tabindex="0" role="row">

<td>Mitigation Implemented</td>

<td>0</td>

</tr>

<tr tabindex="0" role="row">

<td>Total</td>

<td>37</td>

</tr>

<tr tabindex="0" role="row">

<td>Total Migrated</td>

<td>0</td>

</tr>

</tbody>

</table>

### Interaction: Request

![Request interaction screenshot
      ](data:image/png;base64,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)

<div class="threat">

#### <span>1\. An adversary can leverage the weak scalability of token cache and cause DoS</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Denial of Service</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">The default cache that ADAL (Active Directory Authentication Library) uses is an in-memory cache that relies on a static store, available process-wide. While this works for native applications, it does not scale for mid tier and backend applications. This can cause availability issues and result in denial of service either by the influence of an adversary or by the large scale of application's users.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Override the default ADAL token cache with a scalable alternative. Refer: <a href="https://aka.ms/tmtauthn#adal-scalable">https://aka.ms/tmtauthn#adal-scalable</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Design</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>2\. An adversary can gain unauthorized access to resources in an Azure subscription</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can gain unauthorized access to resources in Azure subscription. The adversary can be either a disgruntled internal user, or someone who has stolen the credentials of an Azure subscription.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Enable fine-grained access management to Azure Subscription using RBAC. Refer: <a href="https://aka.ms/tmtauthz#grained-rbac">https://aka.ms/tmtauthz#grained-rbac</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Design</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>3\. An adversary can bypass authentication due to non-standard Azure AD authentication schemes</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Spoofing</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can bypass authentication due to non-standard Azure AD authentication schemes</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Use standard authentication scenarios supported by Azure Active Directory. Refer: <a href="https://aka.ms/tmtauthn#authn-aad">https://aka.ms/tmtauthn#authn-aad</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>4\. An adversary may spoof an Azure administrator and gain access to Azure subscription portal</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Spoofing</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may spoof an Azure administrator and gain access to Azure subscription portal if the administrator's credentials are compromised.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Enable fine-grained access management to Azure Subscription using RBAC. Refer: <a href="https://aka.ms/tmtauthz#grained-rbac">https://aka.ms/tmtauthz#grained-rbac</a> Enable Azure Multi-Factor Authentication for Azure Administrators. Refer: <a href="https://aka.ms/tmtauthn#multi-factor-azure-admin">https://aka.ms/tmtauthn#multi-factor-azure-admin</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Design</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>5\. An adversary can get access to a user's session by replaying authentication tokens</span>   [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Spoofing</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can get access to a user's session by replaying authentication tokens</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Ensure that TokenReplayCache is used to prevent the replay of ADAL authentication tokens. Refer: <a href="https://aka.ms/tmtauthn#tokenreplaycache-adal">https://aka.ms/tmtauthn#tokenreplaycache-adal</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Request

![Request interaction screenshot
      ](data:image/png;base64,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)

<div class="threat">

#### <span>6\. An adversary may block access to the application or API hosted on Azure App Service API App through a denial of service attack</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Denial of Service</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may block access to the application or API hosted on Azure App Service API App through a denial of service attack</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Network level denial of service mitigations are automatically enabled as part of the Azure platform (Basic Azure DDoS Protection). Refer: <a href="https://aka.ms/tmt-th165a">https://aka.ms/tmt-th165a</a>. Implement application level throttling (e.g. per-user, per-session, per-API) to maintain service availability and protect against DoS attacks. Leverage Azure API Management for managing and protecting APIs. Refer: <a href="https://aka.ms/tmt-th165b">https://aka.ms/tmt-th165b</a>. General throttling guidance, refer: <a href="https://aka.ms/tmt-th165c">https://aka.ms/tmt-th165c</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>7\. An adversary may gain long term persistent access to related resources through the compromise of an application identity</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may gain long term persistent access to related resources through the compromise of an application identity</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Store secrets in secret storage solutions where possible, and rotate secrets on a regular cadence. Use Managed Service Identity to create a managed app identity on Azure Active Directory and use it to access AAD-protected resources. Refer: <a href="https://aka.ms/tmt-th166">https://aka.ms/tmt-th166</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>8\. An adversary may gain unauthorized access to Azure App Service API App due to weak network configuration</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may gain unauthorized access to Azure App Service API App due to weak network configuration</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Restrict access to Azure App Service to selected networks (e.g. IP whitelisting, VNET integrations). Refer: <a href="https://aka.ms/tmt-th167">https://aka.ms/tmt-th167</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>9\. An adversary may get access to a user's session due to improper logout from Azure AD</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may get access to a user's session due to improper logout from Azure AD</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Implement proper logout using ADAL methods when using Azure AD. Refer: <a href="https://aka.ms/tmt-th172">https://aka.ms/tmt-th172</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>10\. An adversary may perform action(s) on behalf of another user due to lack of controls against cross domain requests</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may perform action(s) on behalf of another user due to lack of controls against cross domain requests</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Ensure that only trusted origins are allowed if CORS is being used. Refer: <a href="https://aka.ms/tmt-th176">https://aka.ms/tmt-th176</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Request

![Request interaction screenshot
      ](data:image/png;base64,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)

<div class="threat">

#### <span>11\. An adversary can gain unauthorized access to Azure Key Vault instances due to weak network security configuration.</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can gain unauthorized access to Azure Key Vault instances due to weak network security configuration.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Restrict access to Azure Key Vault instances by configuring firewall rules to permit connections from selected networks (e.g. a virtual network or a custom set of IP addresses).For Key Vault client applications behind a firewall trying to access a Key Vault instance, see best practices mentioned here: <a href="https://aka.ms/tmt-th179 ">https://aka.ms/tmt-th179 </a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>12\. An adversary can deny actions performed on Azure Key Vault due to a lack of auditing.</span>   [State: Not Started]  [Priority: Medium] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Repudiation</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can deny actions performed on Azure Key Vault due to a lack of auditing.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Enable audit logging on Azure Key Vault instances to monitor how and when the instances are access, and by whom. Use standard Azure access controls to restrict access to the logs. Refer : <a href="https://aka.ms/tmt-th180 ">https://aka.ms/tmt-th180 </a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>13\. An adversary may gain unauthorized access to manage Azure Key Vault due to weak authorization rules.</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may gain unauthorized access to manage Azure Key Vault due to weak authorization rules.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Access to the Azure Key Vault management plane should be restricted by choosing appropriate Role-Based Access Control (RBAC) roles and privileges in accordance with the principle of least privilege. Over permissive or weak authorization rules may potentially permit data plane access (e.g. a user with Contribute (RBAC) permissions to Key Vault management plane may grant themselves access to the data plane by setting the Azure Key Vault access policy). Refer : <a href="https://aka.ms/tmt-th181 ">https://aka.ms/tmt-th181 </a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>14\. An adversary may gain unauthorized access to Azure Key Vault secrets due to weak authorization rules</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may gain unauthorized access to Azure Key Vault secrets due to weak authorization rules</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Limit Azure Key Vault data plane access by configuring strict access policies. Grant users, groups and applications the ability to perform only the necessary operations against keys or secrets in a Key Vault instance. Follow the principle of least privilege and grant privileges only as needed. Refer : <a href="https://aka.ms/tmt-th181 ">https://aka.ms/tmt-th181 </a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>15\. An adversary can abuse poorly managed authentication/access policies. An adversary may gain unauthorized access to Azure Key Vault due to compromise of secret/certificate used to authenticate to Azure Key Vault .</span>   [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can abuse poorly managed authentication/access policies. An adversary may gain unauthorized access to Azure Key Vault due to compromise of secret/certificate used to authenticate to Azure Key Vault .</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Use managed identities for Azure resources and details can be found here at <a href="https://aka.ms/tmt-th183 ">https://aka.ms/tmt-th183 </a>. If managed identities is not supported , use Service/User Principal and Certificate. If none of the above options are feasible, please ensure secure management and storage of Azure Key Vault Service/User Principal secret . It is recommended to rotate service/user principal secret regularly, in accordance with organizational policies.</td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>16\. An adversary may attempt to delete key vault or key vault object causing business disruption.</span>   [State: Not Started]  [Priority: Low] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Denial of Service</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may attempt to delete key vault or key vault object causing business disruption.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Key Vault's soft delete feature allows recovery of the deleted vaults and vault objects, known as soft-delete . Soft deleted resources are retained for a set period of time, 90 days. Refer : <a href="https://aka.ms/tmt-th186 ">https://aka.ms/tmt-th186 </a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Request

![Request interaction screenshot
      ](data:image/png;base64,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)

<div class="threat">

#### <span>17\. An adversary can gain unauthorized access to Azure SQL database due to weak account policy</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">Due to poorly configured account policies, adversary can launch brute force attacks on Azure SQL Database</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> When possible use Azure Active Directory Authentication for connecting to SQL Database. Refer: <a href="https://aka.ms/tmt-th10a">https://aka.ms/tmt-th10a</a> Ensure that least-privileged accounts are used to connect to Database server. Refer: <a href="https://aka.ms/tmt-th10b">https://aka.ms/tmt-th10b</a> and <a href="https://aka.ms/tmt-th10c">https://aka.ms/tmt-th10c</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>18\. An adversary can gain unauthorized access to Azure SQL DB instances due to weak network security configuration.</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can gain unauthorized access to Azure SQL DB instances due to weak network security configuration.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Restrict access to Azure SQL Database instances by configuring server-level and database-level firewall rules to permit connections from selected networks (e.g. a virtual network or a custom set of IP addresses) where possible. Refer:<a href="https://aka.ms/tmt-th143">https://aka.ms/tmt-th143</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>19\. An adversary can read confidential data due to weak connection string configuration</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Information Disclosure</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can read confidential data due to weak connection string configuration.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Clients connecting to an Azure SQL Database instance using a connection string should ensure encrypt=true and trustservercertificate=false are set. This configuration ensures that connections are encrypted only if there is a verifiable server certificate (otherwise the connection attempt fails). This helps protect against Man-In-The-Middle attacks. Refer: <a href="https://aka.ms/tmt-th144">https://aka.ms/tmt-th144</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>20\. An adversary having access to the storage container (e.g. physical access to the storage media) may be able to read sensitive data</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Information Disclosure</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary having access to the storage container (e.g. physical access to the storage media) may be able to read sensitive data.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Enable Transparent Data Encryption (TDE) on Azure SQL Database instances to have data encrypted at rest. Refer:<a href="https://aka.ms/tmt-th145a">https://aka.ms/tmt-th145a</a>. Use the Always Encrypted feature to allow client applications to encrypt sensitive data before it is sent to the Azure SQL Database. Refer: <a href="https://aka.ms/tmt-th145b">https://aka.ms/tmt-th145b</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>21\. A compromised identity may permit more privileges than intended to an adversary due to weak permission and role assignments</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">A compromised identity may permit more privileges than intended to an adversary due to weak permission and role assignments.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> It is recommended to review permission and role assignments to ensure the users are granted the least privileges necessary. Refer: <a href="https://aka.ms/tmt-th146">https://aka.ms/tmt-th146</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>22\. An adversary can deny actions performed on Azure SQL Database due to a lack of auditing</span>  [State: Not Started]  [Priority: Medium] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Repudiation</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can deny actions performed on Azure SQL Database due to a lack of auditing.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Enable auditing on Azure SQL Database instances to track and log database events. After configuring and customizing the audited events, enable threat detection to receive alerts on anomalous database activities indicating potential security threats. Refer: <a href="https://aka.ms/tmt-th147">https://aka.ms/tmt-th147</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Design</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>23\. An adversary can gain long term, persistent access to an Azure SQL DB instance through the compromise of local user account password(s)</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can gain long term, persistent access to an Azure SQL DB instance through the compromise of local user account password(s).</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> It is recommended to rotate user account passwords (e.g. those used in connection strings) regularly, in accordance with your organization's policies. Store secrets in a secret storage solution (e.g. Azure Key Vault).</td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>24\. An adversary may abuse weak Azure SQL Database configuration</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may abuse weak Azure SQL Database configuration.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Enable SQL Vulnerability Assessment to gain visibility into the security posture of your Azure SQL Database instances. Acting on the assessment results help reduce attack surface and enhance your database security. Refer: <a href="https://aka.ms/tmt-th149">https://aka.ms/tmt-th149</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Response

![Response interaction screenshot
      ](data:image/png;base64,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)

<div class="threat">

#### <span>25\. An adversary can gain unauthorized access to resources in an Azure subscription</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can gain unauthorized access to resources in Azure subscription. The adversary can be either a disgruntled internal user, or someone who has stolen the credentials of an Azure subscription.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Enable fine-grained access management to Azure Subscription using RBAC. Refer: <a href="https://aka.ms/tmtauthz#grained-rbac">https://aka.ms/tmtauthz#grained-rbac</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Design</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>26\. An adversary may spoof an Azure administrator and gain access to Azure subscription portal</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Spoofing</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may spoof an Azure administrator and gain access to Azure subscription portal if the administrator's credentials are compromised.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Enable fine-grained access management to Azure Subscription using RBAC. Refer: <a href="https://aka.ms/tmtauthz#grained-rbac">https://aka.ms/tmtauthz#grained-rbac</a> Enable Azure Multi-Factor Authentication for Azure Administrators. Refer: <a href="https://aka.ms/tmtauthn#multi-factor-azure-admin">https://aka.ms/tmtauthn#multi-factor-azure-admin</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Design</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Response

![Response interaction screenshot
      ](data:image/png;base64,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)

<div class="threat">

#### <span>27\. An adversary can leverage the weak scalability of token cache and cause DoS</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Denial of Service</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">The default cache that ADAL (Active Directory Authentication Library) uses is an in-memory cache that relies on a static store, available process-wide. While this works for native applications, it does not scale for mid tier and backend applications. This can cause availability issues and result in denial of service either by the influence of an adversary or by the large scale of application's users.</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Override the default ADAL token cache with a scalable alternative. Refer: <a href="https://aka.ms/tmtauthn#adal-scalable">https://aka.ms/tmtauthn#adal-scalable</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Design</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>28\. An adversary can bypass authentication due to non-standard Azure AD authentication schemes</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Spoofing</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can bypass authentication due to non-standard Azure AD authentication schemes</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Use standard authentication scenarios supported by Azure Active Directory. Refer: <a href="https://aka.ms/tmtauthn#authn-aad">https://aka.ms/tmtauthn#authn-aad</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>29\. An adversary can get access to a user's session by replaying authentication tokens</span>   [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Spoofing</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary can get access to a user's session by replaying authentication tokens</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Ensure that TokenReplayCache is used to prevent the replay of ADAL authentication tokens. Refer: <a href="https://aka.ms/tmtauthn#tokenreplaycache-adal">https://aka.ms/tmtauthn#tokenreplaycache-adal</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Response

![Response interaction screenshot
      ](data:image/png;base64,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)

<div class="threat">

#### <span>30\. An adversary may block access to the application or API hosted on Azure App Service API App through a denial of service attack</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Denial of Service</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may block access to the application or API hosted on Azure App Service API App through a denial of service attack</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Network level denial of service mitigations are automatically enabled as part of the Azure platform (Basic Azure DDoS Protection). Refer: <a href="https://aka.ms/tmt-th165a">https://aka.ms/tmt-th165a</a>. Implement application level throttling (e.g. per-user, per-session, per-API) to maintain service availability and protect against DoS attacks. Leverage Azure API Management for managing and protecting APIs. Refer: <a href="https://aka.ms/tmt-th165b">https://aka.ms/tmt-th165b</a>. General throttling guidance, refer: <a href="https://aka.ms/tmt-th165c">https://aka.ms/tmt-th165c</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>31\. An adversary may gain long term persistent access to related resources through the compromise of an application identity</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may gain long term persistent access to related resources through the compromise of an application identity</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Store secrets in secret storage solutions where possible, and rotate secrets on a regular cadence. Use Managed Service Identity to create a managed app identity on Azure Active Directory and use it to access AAD-protected resources. Refer: <a href="https://aka.ms/tmt-th166">https://aka.ms/tmt-th166</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>32\. An adversary may gain unauthorized access to Azure App Service API App due to weak network configuration</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may gain unauthorized access to Azure App Service API App due to weak network configuration</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Restrict access to Azure App Service to selected networks (e.g. IP whitelisting, VNET integrations). Refer: <a href="https://aka.ms/tmt-th167">https://aka.ms/tmt-th167</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>33\. An adversary may perform action(s) on behalf of another user due to lack of controls against cross domain requests</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may perform action(s) on behalf of another user due to lack of controls against cross domain requests</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Ensure that only trusted origins are allowed if CORS is being used. Refer: <a href="https://aka.ms/tmt-th176">https://aka.ms/tmt-th176</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Response

![Response interaction screenshot
      ](data:image/png;base64,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)

<div class="threat">

#### <span>34\. An adversary may block access to the application or API hosted on Azure App Service API App through a denial of service attack</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Denial of Service</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may block access to the application or API hosted on Azure App Service API App through a denial of service attack</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Network level denial of service mitigations are automatically enabled as part of the Azure platform (Basic Azure DDoS Protection). Refer: <a href="https://aka.ms/tmt-th165a">https://aka.ms/tmt-th165a</a>. Implement application level throttling (e.g. per-user, per-session, per-API) to maintain service availability and protect against DoS attacks. Leverage Azure API Management for managing and protecting APIs. Refer: <a href="https://aka.ms/tmt-th165b">https://aka.ms/tmt-th165b</a>. General throttling guidance, refer: <a href="https://aka.ms/tmt-th165c">https://aka.ms/tmt-th165c</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>35\. An adversary may gain long term persistent access to related resources through the compromise of an application identity</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may gain long term persistent access to related resources through the compromise of an application identity</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Store secrets in secret storage solutions where possible, and rotate secrets on a regular cadence. Use Managed Service Identity to create a managed app identity on Azure Active Directory and use it to access AAD-protected resources. Refer: <a href="https://aka.ms/tmt-th166">https://aka.ms/tmt-th166</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>36\. An adversary may gain unauthorized access to Azure App Service API App due to weak network configuration</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may gain unauthorized access to Azure App Service API App due to weak network configuration</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Restrict access to Azure App Service to selected networks (e.g. IP whitelisting, VNET integrations). Refer: <a href="https://aka.ms/tmt-th167">https://aka.ms/tmt-th167</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

<div class="threat">

#### <span>37\. An adversary may perform action(s) on behalf of another user due to lack of controls against cross domain requests</span>  [State: Not Started]  [Priority: High] 

<table role="grid">

<tbody>

<tr>

<td id="threat-title-category" role="rowheader" tabindex="0">**Category:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-category">Elevation of Privileges</td>

</tr>

<tr>

<td id="threat-title-description" role="rowheader" tabindex="0">**Description:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-description">An adversary may perform action(s) on behalf of another user due to lack of controls against cross domain requests</td>

</tr>

<tr>

<td id="threat-title-justification" role="rowheader" tabindex="0">**Justification:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-justification"><no mitigation provided></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**Possible Mitigation(s):**</td>

<td tabindex="0" role="gridcell" headers="threat-title-property"><style scoped="scoped">p { margin : 2px; }</style> Ensure that only trusted origins are allowed if CORS is being used. Refer: <a href="https://aka.ms/tmt-th176">https://aka.ms/tmt-th176</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>
