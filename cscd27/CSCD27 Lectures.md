# CSCD27

## Lecture Notes

### LEC 1: Thursday, September 6, 2019

#### Definitions

**Safety:** Satisfies specifications

**Security:** Resists attacks

**Security Theature:**

![security theatre](/Users/joshuaconcon/notes/cscd27/security theatre.png)

**CIA Security Properties:**

- **Confidentiality:** Information is disclosed to legitimate users
- **Integrity:** Information is created or modified by legitimate users
- **Availability:** Information is accessible to legitimate users

**The properties can be conflicting:**

- **Anonymity:** "Do not record the identity of the user that performed an action"
- **Accountability: **"Knowing that someone has done an action"
- **Non-repudation:** "Someone cannot deny having done an action"

Security is often a Compromise

|                            | System         | Security                          |
| -------------------------- | -------------- | --------------------------------- |
| What is it supposed to do? | Specification  | Risk Analysis and Security Policy |
| How does it do it?         | Implementation | Mechanisms                        |
| Does it really do it?      | Validation     | Assurance                         |

**Risk Analysis and Security Policy**

- Goal: Inferring what can go wring with the system
- Outcome: Set of security goals
- Principles: You never prevent a threat, you lower a risk. Performing an attack is more or less difficult the assets to protect vs the attacker's efforts

**Mechanisms**

- Goal: Define a strategy to realize the security goals
- Outcome: Set of security mechanisms
- Principle: Deploying security mechanisms has a cost (cost of recovering vs cost of deployment)

**Assurance**

- Goal: Make sure that the security mechanisms realize the security goals
- Outcome: Methodology
- Principle: Full assurance cannot be achieved.

#### Risk Management Analysis of Security

- You can never prevent a threat, you can only lower the risk
- Performing an attack is more or less difficult 
  - the asset to protect vs the attacker's efforts
- Deploying a counter-measure has a cost
  - cost of recoverying vs cost of deployment

Risk Exposure $=$ probability $\times$ impact

