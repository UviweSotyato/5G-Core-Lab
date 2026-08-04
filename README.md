# 5G Core Network Laboratory

A hands-on 5G Standalone (5G SA) laboratory focused on exploring, deploying, and troubleshooting open-source 5G Core network infrastructure using **Free5GC**.

This repository documents my practical experience working with 5G Core Networks, including deployment, configuration, network-function connectivity, subscriber management, and troubleshooting.

> **Note:** This repository documents my personal technical learning and laboratory work. It does not contain proprietary or confidential information from any organization or employer.

---

## 🚀 Overview

This project serves as a technical record of my hands-on work with 5G Core Network technologies.

The laboratory environment is used to explore how the components of a 5G Standalone network interact, how network functions communicate with one another, and how connectivity issues can be diagnosed and resolved.

The primary 5G Core platform used in this laboratory is **Free5GC**.

---

## 🏗️ Technologies

| Technology    | Purpose                           |
| ------------- | --------------------------------- |
| Free5GC       | 5G Core Network                   |
| 5G Standalone | Mobile network architecture       |
| Linux         | Laboratory environment            |
| MongoDB       | Subscriber and network data       |
| Go            | Free5GC development environment   |
| UERANSIM      | 5G UE and RAN simulation          |
| Git           | Version control and documentation |

---

## 📡 5G Core Architecture

The laboratory explores the major components of a 5G Standalone Core Network, including:

* AMF — Access and Mobility Management Function
* SMF — Session Management Function
* UPF — User Plane Function
* NRF — Network Repository Function
* AUSF — Authentication Server Function
* UDM — Unified Data Management
* UDR — Unified Data Repository
* PCF — Policy Control Function
* NSSF — Network Slice Selection Function

The general architecture explored in the laboratory is:

```text
                    5G Standalone Core

                         ┌─────────┐
                         │   AMF   │
                         └────┬────┘
                              │
                         ┌────▼────┐
                         │   SMF   │
                         └────┬────┘
                              │
                         ┌────▼────┐
                         │   UPF   │
                         └────┬────┘
                              │
                           Data
                           Network
```

A more detailed architecture diagram can be found in:

`diagrams/`

---

## 🧪 Practical Experience

Through this laboratory, I have worked with:

* Deploying a 5G Standalone Core Network using Free5GC
* Configuring and starting 5G Core Network Functions
* Working with subscriber configuration
* Investigating UE registration issues
* Troubleshooting Network Function communication
* Investigating SBI connectivity
* Working with PFCP communication
* Troubleshooting UPF connectivity
* Working with MongoDB and subscriber data
* Using Linux networking tools to diagnose connectivity problems
* Exploring the relationship between the 5G Control Plane and User Plane

---

## 🔧 Troubleshooting Experience

Some of the technical issues investigated during the laboratory include:

### UE Registration

Investigating situations where a User Equipment device could not successfully register with the 5G Core.

Areas investigated include:

* Subscriber configuration
* AMF connectivity
* Authentication procedures
* Network Function communication

### SBI Communication

Investigating communication between 5G Core Network Functions over the Service-Based Interface (SBI).

### PFCP Connectivity

Investigating communication between the SMF and UPF using the Packet Forwarding Control Protocol (PFCP).

### UPF Connectivity

Investigating User Plane connectivity and GTP-related communication.

---

## 📂 Repository Structure

```text
5G-Core-Lab/
│
├── README.md
│
├── docs/
│   ├── free5gc.md
│   └── 5g-core-architecture.md
│
├── diagrams/
│   └── 5g-core-architecture.png
│
└── screenshots/
    ├── free5gc-running.png
    ├── webconsole.png
    └── network-functions.png
```

---

## 📚 Documentation

Detailed technical documentation is available in the `docs` directory.

### Free5GC

Documentation covering the deployment and configuration of the Free5GC 5G Core.

`docs/free5gc.md`

### 5G Core Architecture

Documentation explaining the architecture and interaction between the different 5G Core Network Functions.

`docs/5g-core-architecture.md`

---

## 🖥️ Laboratory Evidence

Screenshots and diagrams demonstrating the laboratory environment and practical work are stored in:

`screenshots/`

and

`diagrams/`

These materials are intended to demonstrate practical hands-on experience while excluding confidential or proprietary information.

---

## 🎯 Current Focus

The current focus of this laboratory is developing practical knowledge in:

* 5G Standalone Core Networks
* 5G Core Network Functions
* Mobile Network Architecture
* Linux Networking
* Network Troubleshooting
* 5G Protocols and Interfaces
* Telecommunications Infrastructure

---

## 🔭 Future Areas of Exploration

Future work may include exploring:

* srsRAN
* UERANSIM
* IMS
* SIP
* VoNR
* Network slicing
* Network monitoring
* Network automation
* Infrastructure as Code

---

## 👨🏾‍💻 About Me

I am a Software Engineer and aspiring Network Automation Engineer with interests spanning software development, networking, telecommunications, and programmable infrastructure.

My technical interests include:

* Network Engineering
* Network Automation
* 5G and Telecommunications
* Web Development
* Mobile Application Development
* Software Engineering

This repository represents part of my journey toward combining software engineering with network infrastructure and automation.

---

## 📫 Connect

**GitHub:** [UviweSotyato](https://github.com/UviweSotyato)

More projects and technical work can be found across my GitHub profile.
