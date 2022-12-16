# Threat Modelling Session with Microsoft

## The CIA Security Trident Distilled

<p align="center" background-color="white">
<img src="./images/cia_triad.png?sanitize=true" width="250px" />
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

<img src="./images/image1.png?sanitize=true" />

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

<img src="./images/image2.png?sanitize=true" />
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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Override the default ADAL token cache with a scalable alternative. Refer: <a href="https://aka.ms/tmtauthn#adal-scalable">https://aka.ms/tmtauthn#adal-scalable</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Enable fine-grained access management to Azure Subscription using RBAC. Refer: <a href="https://aka.ms/tmtauthz#grained-rbac">https://aka.ms/tmtauthz#grained-rbac</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Use standard authentication scenarios supported by Azure Active Directory. Refer: <a href="https://aka.ms/tmtauthn#authn-aad">https://aka.ms/tmtauthn#authn-aad</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Enable fine-grained access management to Azure Subscription using RBAC. Refer: <a href="https://aka.ms/tmtauthz#grained-rbac">https://aka.ms/tmtauthz#grained-rbac</a> Enable Azure Multi-Factor Authentication for Azure Administrators. Refer: <a href="https://aka.ms/tmtauthn#multi-factor-azure-admin">https://aka.ms/tmtauthn#multi-factor-azure-admin</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Ensure that TokenReplayCache is used to prevent the replay of ADAL authentication tokens. Refer: <a href="https://aka.ms/tmtauthn#tokenreplaycache-adal">https://aka.ms/tmtauthn#tokenreplaycache-adal</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Request

<img src="./images/image3.png?sanitize=true" />

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Network level denial of service mitigations are automatically enabled as part of the Azure platform (Basic Azure DDoS Protection). Refer: <a href="https://aka.ms/tmt-th165a">https://aka.ms/tmt-th165a</a>. Implement application level throttling (e.g. per-user, per-session, per-API) to maintain service availability and protect against DoS attacks. Leverage Azure API Management for managing and protecting APIs. Refer: <a href="https://aka.ms/tmt-th165b">https://aka.ms/tmt-th165b</a>. General throttling guidance, refer: <a href="https://aka.ms/tmt-th165c">https://aka.ms/tmt-th165c</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Store secrets in secret storage solutions where possible, and rotate secrets on a regular cadence. Use Managed Service Identity to create a managed app identity on Azure Active Directory and use it to access AAD-protected resources. Refer: <a href="https://aka.ms/tmt-th166">https://aka.ms/tmt-th166</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Restrict access to Azure App Service to selected networks (e.g. IP whitelisting, VNET integrations). Refer: <a href="https://aka.ms/tmt-th167">https://aka.ms/tmt-th167</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Implement proper logout using ADAL methods when using Azure AD. Refer: <a href="https://aka.ms/tmt-th172">https://aka.ms/tmt-th172</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Ensure that only trusted origins are allowed if CORS is being used. Refer: <a href="https://aka.ms/tmt-th176">https://aka.ms/tmt-th176</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Request

<img src="./images/image4.png?sanitize=true" />

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Restrict access to Azure Key Vault instances by configuring firewall rules to permit connections from selected networks (e.g. a virtual network or a custom set of IP addresses).For Key Vault client applications behind a firewall trying to access a Key Vault instance, see best practices mentioned here: <a href="https://aka.ms/tmt-th179 ">https://aka.ms/tmt-th179 </a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Enable audit logging on Azure Key Vault instances to monitor how and when the instances are access, and by whom. Use standard Azure access controls to restrict access to the logs. Refer : <a href="https://aka.ms/tmt-th180 ">https://aka.ms/tmt-th180 </a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Access to the Azure Key Vault management plane should be restricted by choosing appropriate Role-Based Access Control (RBAC) roles and privileges in accordance with the principle of least privilege. Over permissive or weak authorization rules may potentially permit data plane access (e.g. a user with Contribute (RBAC) permissions to Key Vault management plane may grant themselves access to the data plane by setting the Azure Key Vault access policy). Refer : <a href="https://aka.ms/tmt-th181 ">https://aka.ms/tmt-th181 </a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Limit Azure Key Vault data plane access by configuring strict access policies. Grant users, groups and applications the ability to perform only the necessary operations against keys or secrets in a Key Vault instance. Follow the principle of least privilege and grant privileges only as needed. Refer : <a href="https://aka.ms/tmt-th181 ">https://aka.ms/tmt-th181 </a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Use managed identities for Azure resources and details can be found here at <a href="https://aka.ms/tmt-th183 ">https://aka.ms/tmt-th183 </a>. If managed identities is not supported , use Service/User Principal and Certificate. If none of the above options are feasible, please ensure secure management and storage of Azure Key Vault Service/User Principal secret . It is recommended to rotate service/user principal secret regularly, in accordance with organizational policies.</td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Key Vault's soft delete feature allows recovery of the deleted vaults and vault objects, known as soft-delete . Soft deleted resources are retained for a set period of time, 90 days. Refer : <a href="https://aka.ms/tmt-th186 ">https://aka.ms/tmt-th186 </a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Request

<img src="./images/image5.png?sanitize=true" />

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> When possible use Azure Active Directory Authentication for connecting to SQL Database. Refer: <a href="https://aka.ms/tmt-th10a">https://aka.ms/tmt-th10a</a> Ensure that least-privileged accounts are used to connect to Database server. Refer: <a href="https://aka.ms/tmt-th10b">https://aka.ms/tmt-th10b</a> and <a href="https://aka.ms/tmt-th10c">https://aka.ms/tmt-th10c</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Restrict access to Azure SQL Database instances by configuring server-level and database-level firewall rules to permit connections from selected networks (e.g. a virtual network or a custom set of IP addresses) where possible. Refer:<a href="https://aka.ms/tmt-th143">https://aka.ms/tmt-th143</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Clients connecting to an Azure SQL Database instance using a connection string should ensure encrypt=true and trustservercertificate=false are set. This configuration ensures that connections are encrypted only if there is a verifiable server certificate (otherwise the connection attempt fails). This helps protect against Man-In-The-Middle attacks. Refer: <a href="https://aka.ms/tmt-th144">https://aka.ms/tmt-th144</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Enable Transparent Data Encryption (TDE) on Azure SQL Database instances to have data encrypted at rest. Refer:<a href="https://aka.ms/tmt-th145a">https://aka.ms/tmt-th145a</a>. Use the Always Encrypted feature to allow client applications to encrypt sensitive data before it is sent to the Azure SQL Database. Refer: <a href="https://aka.ms/tmt-th145b">https://aka.ms/tmt-th145b</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> It is recommended to review permission and role assignments to ensure the users are granted the least privileges necessary. Refer: <a href="https://aka.ms/tmt-th146">https://aka.ms/tmt-th146</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Enable auditing on Azure SQL Database instances to track and log database events. After configuring and customizing the audited events, enable threat detection to receive alerts on anomalous database activities indicating potential security threats. Refer: <a href="https://aka.ms/tmt-th147">https://aka.ms/tmt-th147</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> It is recommended to rotate user account passwords (e.g. those used in connection strings) regularly, in accordance with your organization's policies. Store secrets in a secret storage solution (e.g. Azure Key Vault).</td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Enable SQL Vulnerability Assessment to gain visibility into the security posture of your Azure SQL Database instances. Acting on the assessment results help reduce attack surface and enhance your database security. Refer: <a href="https://aka.ms/tmt-th149">https://aka.ms/tmt-th149</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Response

<img src="./images/image6.png?sanitize=true" />

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Enable fine-grained access management to Azure Subscription using RBAC. Refer: <a href="https://aka.ms/tmtauthz#grained-rbac">https://aka.ms/tmtauthz#grained-rbac</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Enable fine-grained access management to Azure Subscription using RBAC. Refer: <a href="https://aka.ms/tmtauthz#grained-rbac">https://aka.ms/tmtauthz#grained-rbac</a> Enable Azure Multi-Factor Authentication for Azure Administrators. Refer: <a href="https://aka.ms/tmtauthn#multi-factor-azure-admin">https://aka.ms/tmtauthn#multi-factor-azure-admin</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Design</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Response

<img src="./images/image7.png?sanitize=true" />

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Override the default ADAL token cache with a scalable alternative. Refer: <a href="https://aka.ms/tmtauthn#adal-scalable">https://aka.ms/tmtauthn#adal-scalable</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Use standard authentication scenarios supported by Azure Active Directory. Refer: <a href="https://aka.ms/tmtauthn#authn-aad">https://aka.ms/tmtauthn#authn-aad</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Ensure that TokenReplayCache is used to prevent the replay of ADAL authentication tokens. Refer: <a href="https://aka.ms/tmtauthn#tokenreplaycache-adal">https://aka.ms/tmtauthn#tokenreplaycache-adal</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Response
<img src="./images/image8.png?sanitize=true" />

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Network level denial of service mitigations are automatically enabled as part of the Azure platform (Basic Azure DDoS Protection). Refer: <a href="https://aka.ms/tmt-th165a">https://aka.ms/tmt-th165a</a>. Implement application level throttling (e.g. per-user, per-session, per-API) to maintain service availability and protect against DoS attacks. Leverage Azure API Management for managing and protecting APIs. Refer: <a href="https://aka.ms/tmt-th165b">https://aka.ms/tmt-th165b</a>. General throttling guidance, refer: <a href="https://aka.ms/tmt-th165c">https://aka.ms/tmt-th165c</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Store secrets in secret storage solutions where possible, and rotate secrets on a regular cadence. Use Managed Service Identity to create a managed app identity on Azure Active Directory and use it to access AAD-protected resources. Refer: <a href="https://aka.ms/tmt-th166">https://aka.ms/tmt-th166</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Restrict access to Azure App Service to selected networks (e.g. IP whitelisting, VNET integrations). Refer: <a href="https://aka.ms/tmt-th167">https://aka.ms/tmt-th167</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Ensure that only trusted origins are allowed if CORS is being used. Refer: <a href="https://aka.ms/tmt-th176">https://aka.ms/tmt-th176</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>

### Interaction: Response

<img src="./images/image9.png?sanitize=true" />

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Network level denial of service mitigations are automatically enabled as part of the Azure platform (Basic Azure DDoS Protection). Refer: <a href="https://aka.ms/tmt-th165a">https://aka.ms/tmt-th165a</a>. Implement application level throttling (e.g. per-user, per-session, per-API) to maintain service availability and protect against DoS attacks. Leverage Azure API Management for managing and protecting APIs. Refer: <a href="https://aka.ms/tmt-th165b">https://aka.ms/tmt-th165b</a>. General throttling guidance, refer: <a href="https://aka.ms/tmt-th165c">https://aka.ms/tmt-th165c</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Store secrets in secret storage solutions where possible, and rotate secrets on a regular cadence. Use Managed Service Identity to create a managed app identity on Azure Active Directory and use it to access AAD-protected resources. Refer: <a href="https://aka.ms/tmt-th166">https://aka.ms/tmt-th166</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Restrict access to Azure App Service to selected networks (e.g. IP whitelisting, VNET integrations). Refer: <a href="https://aka.ms/tmt-th167">https://aka.ms/tmt-th167</a></td>

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

<td tabindex="0" role="gridcell" headers="threat-title-property"> Ensure that only trusted origins are allowed if CORS is being used. Refer: <a href="https://aka.ms/tmt-th176">https://aka.ms/tmt-th176</a></td>

</tr>

<tr>

<td id="threat-title-property" role="rowheader" tabindex="0">**SDL Phase:**</td>

<td class="infotd" tabindex="0" role="gridcell" headers="threat-title-property">Implementation</td>

</tr>

</tbody>

</table>

</div>
