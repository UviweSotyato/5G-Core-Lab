# Free5GC 5G Core Deployment and Troubleshooting

## 1. Introduction

This document records my hands-on experience deploying, configuring, and troubleshooting a 5G Standalone (5G SA) Core Network using Free5GC in a Linux-based laboratory environment.

The objective of this work was to gain practical experience with 5G Core Network architecture and understand how the different Network Functions communicate and operate together.

The work involved deploying Free5GC, configuring the required environment, investigating connectivity issues, and troubleshooting communication between different 5G Core components.

---

# 2. Laboratory Environment

The laboratory environment consists of a Linux-based system used to deploy and test the Free5GC 5G Core.

### Environment

* Operating System: Ubuntu Linux
* 5G Core: Free5GC
* Database: MongoDB
* Programming Language: Go
* Version Control: Git

Additional components used or explored during the laboratory include:

* UERANSIM
* Linux networking utilities
* 5G Core Network Functions
* GTP
* PFCP
* Service-Based Interface (SBI)

---

# 3. Free5GC Architecture

Free5GC implements the core network functions required for a 5G Standalone architecture.

The main Network Functions explored during this work include:

| Network Function | Description                             |
| ---------------- | --------------------------------------- |
| AMF              | Access and Mobility Management Function |
| SMF              | Session Management Function             |
| UPF              | User Plane Function                     |
| NRF              | Network Repository Function             |
| AUSF             | Authentication Server Function          |
| UDM              | Unified Data Management                 |
| UDR              | Unified Data Repository                 |
| PCF              | Policy Control Function                 |
| NSSF             | Network Slice Selection Function        |

The Network Functions communicate using different interfaces and protocols.

For example:

```text
                     5G Core

              ┌─────────────────┐
              │       AMF       │
              └────────┬────────┘
                       │
                       │ SBI
                       │
              ┌────────▼────────┐
              │       SMF       │
              └────────┬────────┘
                       │
                       │ PFCP
                       │
              ┌────────▼────────┐
              │       UPF       │
              └────────┬────────┘
                       │
                       │ GTP-U
                       │
                       ▼
                  Data Network
```

---

# 4. Deployment Process

The Free5GC deployment involved preparing the Linux environment and installing the required dependencies.

The general deployment process consisted of:

1. Preparing the Linux environment
2. Installing required dependencies
3. Installing and configuring MongoDB
4. Obtaining the Free5GC source code
5. Building the Free5GC Network Functions
6. Configuring the 5G Core
7. Starting the Network Functions
8. Verifying Network Function communication
9. Configuring subscriber information
10. Testing User Equipment registration

---

# 5. MongoDB Integration

MongoDB was used as part of the Free5GC deployment to support the storage of network and subscriber-related information.

During the setup process, the database environment was configured and verified to ensure that Free5GC components could communicate with the database successfully.

The database layer is important because subscriber information and other network-related data are required for successful authentication and registration procedures.

---

# 6. Network Function Communication

One of the key areas explored during the deployment was communication between the different 5G Core Network Functions.

The Free5GC architecture relies heavily on communication between Network Functions.

Examples include:

```text
AMF
 │
 ├──── SBI ────▶ NRF
 │
 ├──── SBI ────▶ AUSF
 │
 └──── SBI ────▶ UDM


SMF
 │
 └──── PFCP ────▶ UPF
```

Understanding these communication paths was important when diagnosing network registration and connectivity problems.

---

# 7. UE Registration Troubleshooting

One of the troubleshooting scenarios encountered during the laboratory involved User Equipment registration.

During testing, the UE registration procedure returned an error indicating that the subscriber could not be found.

The issue was investigated by examining:

* Subscriber configuration
* UE configuration
* SUPI information
* Authentication parameters
* Free5GC subscriber data
* Communication between the UE and the 5G Core

This highlighted the importance of ensuring that subscriber information configured on the UE matches the information stored in the 5G Core subscriber database.

The troubleshooting process involved checking the configuration and identifying the mismatch responsible for the registration failure.

---

# 8. PFCP Troubleshooting

Another area investigated during the laboratory was Packet Forwarding Control Protocol (PFCP) communication.

PFCP is used for communication between the Session Management Function (SMF) and User Plane Function (UPF).

The architecture can be represented as:

```text
                Control Plane

                  ┌───────┐
                  │  SMF  │
                  └───┬───┘
                      │
                      │ PFCP
                      │
                  ┌───▼───┐
                  │  UPF  │
                  └───┬───┘
                      │
                      │ GTP-U
                      │
                      ▼
                 User Plane
```

Troubleshooting involved investigating whether the UPF was reachable and whether the required interfaces and ports were correctly configured.

This work provided practical experience in diagnosing communication problems within the 5G Core User Plane.

---

# 9. UPF and GTP Troubleshooting

The User Plane Function is responsible for handling user traffic within the 5G Core.

During the laboratory work, issues involving GTP-related communication and UPF interface binding were investigated.

The troubleshooting process involved examining:

* Network interfaces
* IP addressing
* GTP configuration
* UPF configuration
* Port availability
* Linux networking configuration

Linux networking utilities were used to investigate connectivity and determine where communication problems were occurring.

---

# 10. Service-Based Interface (SBI) Troubleshooting

The 5G Core uses a Service-Based Architecture where Network Functions communicate using service-based interfaces.

During the laboratory work, issues related to SBI communication and Network Function connectivity were investigated.

Troubleshooting involved examining:

* Network Function configuration
* IP addresses
* Ports
* NRF registration
* Service availability
* Network Function logs

Understanding SBI communication was important when determining whether Network Functions were successfully discovering and communicating with one another.

---

# 11. Key Learning Outcomes

Through this practical work, I developed hands-on experience with:

* 5G Standalone architecture
* Free5GC deployment
* 5G Core Network Functions
* Linux-based network infrastructure
* MongoDB integration
* Subscriber management
* UE registration procedures
* Service-Based Architecture
* SBI communication
* PFCP
* GTP
* Control Plane and User Plane concepts
* Network troubleshooting
* Log analysis
* Configuration-based debugging

---

# 12. Challenges and Troubleshooting

Working with a 5G Core Network required troubleshooting across multiple layers of the system.

The main challenges investigated included:

| Problem Area         | Investigation                               |
| -------------------- | ------------------------------------------- |
| UE Registration      | Subscriber and authentication configuration |
| Subscriber Not Found | Subscriber database and UE configuration    |
| SBI Connectivity     | Network Function communication              |
| PFCP                 | SMF and UPF communication                   |
| UPF                  | Interface and User Plane configuration      |
| GTP                  | User Plane connectivity                     |
| MongoDB              | Database availability and integration       |

These challenges provided practical experience in diagnosing complex distributed network systems.

---

# 13. Future Work

Future work will expand the laboratory to explore additional components of the 5G ecosystem.

Planned areas of exploration include:

* UERANSIM integration
* srsRAN integration
* IMS integration
* SIP signaling
* VoNR
* Network slicing
* Network monitoring
* Network performance testing
* Network automation

The long-term goal is to develop a deeper understanding of programmable telecommunications infrastructure and the relationship between software engineering, networking, and 5G systems.

---

# 14. Disclaimer

This repository is intended to document personal technical learning and laboratory experience.

No proprietary, confidential, or restricted information from any employer or organization is included in this documentation.
