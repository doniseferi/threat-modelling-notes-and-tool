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

