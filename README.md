# Threat Modelling Session with Microsoft

## The CIA Security Trident Distilled

<p align="center" background-color="white">
<img src="./cia_triad.png?sanitize=true" width="250px" />
</p>

The CIA trident, confidentiality, integrity and availability are the three pillars of security. _For any resource to be considered secure it must consider and address all sides of the CIA trident._

- Confidentiality is a systems ability to ensure correct access control over data.
- Integrity is a systems ability to ensure data validity.
- Availability is the system's ability to remain running and ensure it is available.

# Confidentiality

For any system to maintain confidentiality it must ensure and enforce correct access control.


# Integrity

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

# Availability

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

### The STRIDE model

1. Spoofing
2. Tampering
3. Repudiation
4. Information disclosure
5. Denial of service
6. Elevation of privileges

### Threat

# Thread Modelling Tool

### How to threat model

When threat modelling follow the following high level steps:
1. Define scope and depth of analysis
2. Produce a visual 
3. 

## Application

Microsoft have made a threat modelling tool available which has been attached to this repository on [this link](./TMT7.application).

### Running Microsoft's threat modelling tool

Running the application is as simple as double clicking the '[TMT7.application](./TMT7.application)' file attached to this repo. 

#### Create a new threat model

To start threat modelling once you have opened the application ensure the 'Template For New Models' is set to 'Azure Threat Model Template (x.x.x)' and click the big azure coloured 'Create A Model' button. Once you have created your model click the reports tab at the top, then the 'Create Full Report' tab and provide the name and location for the model to be saved.

#### Load an existing threat model

Once you have opened the threat modelling application click the big azure coloured 'Open A Model' button and load an already created model, such as the example one provided [here](./DcrModell.tm7).
