# 5G Standalone Core Network Architecture

## 1. Introduction

A 5G Standalone (5G SA) network consists of a 5G Radio Access Network (RAN) connected directly to a 5G Core Network.

Unlike 5G Non-Standalone (NSA), which relies on an existing 4G LTE Core, 5G Standalone uses a dedicated 5G Core designed around a Service-Based Architecture (SBA).

This document describes the architecture explored during my hands-on work with Free5GC and the relationships between the major components of a 5G Standalone network.

---

# 2. High-Level Architecture

The general architecture can be represented as:

```text
                    5G Standalone Network

 ┌───────────┐
 │    UE     │
 │           │
 │ 5G Device │
 └─────┬─────┘
       │
       │ Radio Interface
       │
       ▼
 ┌───────────┐
 │    gNB    │
 │ 5G RAN    │
 └─────┬─────┘
       │
       │ NG Interface
       │
       ▼
 ┌───────────────────────────────────────┐
 │              5G Core                  │
 │                                       │
 │  ┌─────┐  ┌─────┐  ┌─────┐           │
 │  │ AMF │  │ SMF │  │ NRF │           │
 │  └─────┘  └─────┘  └─────┘           │
 │                                       │
 │  ┌─────┐  ┌─────┐  ┌─────┐           │
 │  │AUSF │  │ UDM │  │ UDR │           │
 │  └─────┘  └─────┘  └─────┘           │
 │                                       │
 │  ┌─────┐  ┌─────┐                    │
 │  │ PCF │  │NSSF │                    │
 │  └─────┘  └─────┘                    │
 │                                       │
 │             ┌─────┐                   │
 │             │ UPF │                   │
 │             └──┬──┘                   │
 └────────────────┼──────────────────────┘
                  │
                  │ N6 / User Traffic
                  │
                  ▼
           ┌─────────────┐
           │ Data Network│
           │  Internet   │
           └─────────────┘
```

---

# 3. User Equipment

The User Equipment (UE) represents the device connecting to the 5G network.

Examples include:

* Smartphones
* IoT devices
* Industrial equipment
* 5G routers

In a laboratory environment, the UE can be simulated using software such as UERANSIM.

The UE communicates with the 5G Radio Access Network and initiates procedures such as registration and PDU session establishment.

---

# 4. 5G Radio Access Network

The 5G Radio Access Network is represented by the gNB.

The gNB provides the radio connectivity between the UE and the 5G Core.

The gNB communicates with the 5G Core using the NG interface.

The architecture can be simplified as:

```text
UE
 │
 │ 5G Radio
 │
 ▼
gNB
 │
 │ NG Interface
 │
 ▼
5G Core
```

---

# 5. Access and Mobility Management Function

The Access and Mobility Management Function (AMF) is responsible for handling access and mobility-related procedures.

Responsibilities include:

* UE registration
* Connection management
* Mobility management
* NAS signaling
* Authentication coordination

The AMF acts as an important control-plane entry point between the RAN and the 5G Core.

---

# 6. Session Management Function

The Session Management Function (SMF) manages PDU sessions.

Responsibilities include:

* PDU session establishment
* Session modification
* Session release
* IP address allocation
* UPF selection
* UPF control

The SMF communicates with the UPF using PFCP.

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
                  └───────┘

```

---

# 7. User Plane Function

The User Plane Function (UPF) is responsible for forwarding user traffic.

The UPF handles the User Plane of the 5G network.

User traffic flows through the UPF between the UE and external data networks.

```text
UE
 │
 │ User Traffic
 │
 ▼
gNB
 │
 │ N3
 │
 ▼
UPF
 │
 │ N6
 │
 ▼
Data Network
```

The UPF is therefore a critical component when validating end-to-end data connectivity.

---

# 8. Network Repository Function

The Network Repository Function (NRF) provides Network Function discovery.

Network Functions register their services with the NRF.

Other Network Functions can then discover available services.

Conceptually:

```text
             ┌─────────┐
             │   NRF   │
             └────┬────┘
                  │
       ┌──────────┼──────────┐
       │          │          │
       ▼          ▼          ▼
      AMF        SMF        AUSF
```

The NRF is an important component of the Service-Based Architecture.

---

# 9. Authentication Server Function

The Authentication Server Function (AUSF) participates in the authentication process of the UE.

It works together with other Network Functions to authenticate subscribers during network registration.

---

# 10. Unified Data Management

The Unified Data Management (UDM) manages subscriber-related data and supports authentication and registration procedures.

The UDM interacts with the Unified Data Repository (UDR), where subscriber-related information can be stored.

---

# 11. Unified Data Repository

The Unified Data Repository (UDR) provides data storage for subscriber and network information.

In a Free5GC deployment, subscriber-related information is managed through the 5G Core data layer.

---

# 12. Policy Control Function

The Policy Control Function (PCF) provides policy-related control for the 5G network.

It can be involved in:

* Policy decisions
* QoS policies
* Session policies
* Charging-related policies

---

# 13. Network Slice Selection Function

The Network Slice Selection Function (NSSF) assists with selecting the appropriate network slice for a UE.

Network slicing allows a physical network infrastructure to support logically separated networks with different characteristics and requirements.

---

# 14. Service-Based Architecture

One of the defining characteristics of the 5G Core is the Service-Based Architecture.

Instead of relying entirely on traditional point-to-point interfaces, Network Functions expose services that can be consumed by other Network Functions.

A simplified representation is:

```text
                  Service-Based Architecture

                         ┌─────────┐
                         │   NRF   │
                         └────┬────┘
                              │
             ┌────────────────┼────────────────┐
             │                │                │
             ▼                ▼                ▼
          ┌─────┐          ┌─────┐          ┌─────┐
          │ AMF │          │ SMF │          │AUSF │
          └─────┘          └─────┘          └─────┘
             │                │                │
             └────────────────┼────────────────┘
                              │
                         SBI Communication
```

Understanding SBI communication is important when troubleshooting Network Function discovery and connectivity.

---

# 15. Control Plane and User Plane

The 5G Core can broadly be divided into Control Plane and User Plane functions.

### Control Plane

The Control Plane handles signaling and network control.

Examples include:

* AMF
* SMF
* AUSF
* UDM
* UDR
* PCF
* NRF
* NSSF

### User Plane

The User Plane handles the actual user data traffic.

The primary User Plane component is:

* UPF

The relationship can be summarized as:

```text
                 CONTROL PLANE

UE ────► AMF ────► SMF ────► UPF
         │          │
         │          │ PFCP
         │          │
         ▼          ▼
       AUSF       Policy
       UDM        Control
       UDR
       NRF
       NSSF


                 USER PLANE

UE
 │
 ▼
gNB
 │
 │ N3
 ▼
UPF
 │
 │ N6
 ▼
Internet
```

---

# 16. Key Interfaces

Several interfaces and protocols are important when understanding the 5G Core.

| Interface / Protocol | Purpose                                         |
| -------------------- | ----------------------------------------------- |
| N1                   | UE to AMF signaling                             |
| N2                   | gNB to AMF control-plane signaling              |
| N3                   | gNB to UPF user-plane traffic                   |
| N4                   | SMF to UPF control                              |
| N6                   | UPF to Data Network                             |
| SBI                  | Communication between 5G Core Network Functions |
| PFCP                 | SMF and UPF control                             |
| GTP-U                | User-plane traffic tunneling                    |

These interfaces provide the communication paths required for registration, session establishment, and user-plane connectivity.

---

# 17. Relationship to Free5GC

Free5GC provides an open-source implementation of the 5G Core architecture.

The laboratory environment provides an opportunity to explore how the theoretical concepts of 5G Core architecture translate into practical deployments.

Through hands-on work with Free5GC, I have explored:

* Deployment of 5G Core Network Functions
* Network Function communication
* Subscriber management
* UE registration
* SBI connectivity
* PFCP communication
* UPF configuration
* GTP-related connectivity
* Linux-based network troubleshooting

---

# 18. Practical Understanding

The practical deployment of a 5G Core demonstrates how multiple distributed services must operate together to provide network connectivity.

Troubleshooting requires understanding multiple layers, including:

```text
Application
    │
5G Core Services
    │
SBI / PFCP
    │
IP Networking
    │
Linux Interfaces
    │
Physical / Virtual Infrastructure
```

This layered approach is essential when diagnosing failures in complex telecommunications systems.

---

# 19. Future Exploration

Future exploration of this laboratory environment may include:

* UERANSIM integration
* srsRAN integration
* IMS architecture
* SIP signaling
* VoNR
* Network slicing
* 5G performance testing
* Network monitoring
* Network automation

The goal is to continue developing practical experience in 5G telecommunications, network engineering, and programmable network infrastructure.
