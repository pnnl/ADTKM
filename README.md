# ADTKM
ADTKM Disruption-Tolerant Key Management System

## Introduction
This document describes an overview of the architectural pieces of the Disruption Tolerant Key Management (DTKM) system, their design objectives, and implementation details. The objectives and requirements will be provided to help contextualize design decisions. This report is meant to be a living development document that defines the functionality, components, and capabilities of the prototype DTKM system. The specifications in this document drive prototype development efforts; if and when it is necessary to pivot due to development roadblocks, this document will be updated to reflect the direction change and subsequent reasoning.

This document is one of a suite of documents that will be drafted in the lifetime of the DTKM project. While the development of the DTKM prototype system is one of the major objectives of this project, testing and quantifying its performance are equally important. As such, additional reports will be drafted that document system test models, test cases, test plans, and performance measurements to provide a means to understand the utility of the DTKM approach as compared to existing approaches (such as that in International Electrotechnical Commission (IEC) 62351). Also, as the field of cyber security is ever evolving, these project reports will provide a means by which future extensions and improvements to DTKM concepts can be measured and understood.

### Need
Key management and access control infrastructure are fundamental to building secure systems. However, current key management and trust models were designed for enterprise information technology (IT) environments and do not suit the requirements of supervisory control and data acquisition (SCADA) and distributed control system environments. These environments are geographically distributed with high availability requirements that limit the ability of traditional centralized authentication and authorization mechanisms. Due to operational management difficulties, the lack of a scalable technology to manage cryptographic keys for distributed energy delivery systems (EDSs) hinders asset owners’ deployment of products to secure communications. This problem is amplified as more renewable and distributed energy resources emerge and are integrated into the grid, increasing the number of EDS resources and their complexity. Without an industry-accepted, scalable, secure, and robust key management, authentication, and authorization service that meets operational requirements, development of secure cyber-physical applications will be difficult. Industry requires a cryptographic key and access control management solution to further the deployment of technical solutions and to limit the risk associated with increased communication and functionality of Smart Grid applications. 

The lack of a scalable technology to centrally manage access control and cryptographic keys for EDS hinders the appropriate levels of deployment, configuration, and management of control system security. The base necessity for secure communication is device and individual authentication. Without the ability to assure the identity of communicating parties, the validity of communicated data is unverifiable. Therefore, a method of distributing cryptographic material and authenticating communications is necessary for access control. Without these capabilities, secure system operation is unmanageable. 

The importance of reliable key distribution in this domain flows from the underlying reality that most power distribution components—both controlling and controlled elements—are geographically distributed and, thus, rely on communication channels that span logically and physically accessible public spaces. The current design of the electrical distribution grid is a complex, heterogeneous hierarchy of recent and legacy components—of widely varying sophistication and hardware capability—that has focused more on conservative, safety-centric design than on secure cyber operation principles. Integration of modern cyber security features into control systems represents a significant challenge to vendors, asset owners, and standards bodies. Security solutions can be very complex, often require the deployment of new hardware and software, and can easily be misconfigured without the proper expertise. Given the societal importance of reliable delivery of electrical power, these upgrades require extensive planning, safety review, and testing prior to deployment. Improperly configured security can lead to vulnerabilities (at best) and operational problems (at worst). Operational impact is a major concern because EDSs control critical physical processes; therefore, the cryptographic goals for control systems differ significantly from corporate IT or Internet sites. As a result, substantial design effort has focused on upgrading communications channels to increase their resilience to cyber attacks as they span public spaces. Reliable, secure, and achievable distribution of cryptographic keys is a direct—and critical—part of this methodology. 

Considering the design, scale, and age of most EDSs within the US, a key management solution must provide a roadmap of technology deployment to address the current situation with a path to support the integration of advanced features. The use of cryptography in control systems must support the multiple operational needs of asset owners without adversely affecting safe and reliable operations. These key management methodologies will need to exhibit levels of security that are commensurate with the infrastructure elements they protect and their application must be managed to disallow access to higher security domains from lower ones. Their initial installation and upgrade—both at time of manufacture and in the field—must be sufficiently straightforward for reliable use by the present workforce and, as a system, provide acceptable levels of secure operation across typical field problems such as lost laptops, operator/installer mistakes, and isolated malicious activities. And, lastly, these secure methodologies must be flexible enough to allow alternate control access in cases of natural disaster (e.g., hurricane) or targeted cyber attacks. 

In addition, the access control and key management challenge is made more complicated by the number of vendors creating security products, regulatory requirements to identify and protect critical information, and automation of manual processes. Managing cryptographic keys for a small utility with 30 substations can be done without automation. Managing keys for an automated meter reading environment with millions of smart meters cannot. The operational feasibility of maintaining secure control systems requires that security controls be designed and developed to operate as autonomously as possible to reduce the burden on organizational resources. 

### Impact
The overarching goal of the DTKM project is to design and implement a system to enable the use of cryptographic key management in power distribution substation sensor and control devices, including not just management, but also key verification, updates, and revocation. 

The DTKM system is being designed to accommodate the unique characteristics of EDSs. The approach defined in this document will address and alleviate multiple challenges within the industry. One of the driving requirements is that EDSs often leverage communication infrastructure between geographically separated sites, which must be assumed unreliable. Therefore, the DTKM system is defined such that it can handle periods of disconnected operation without significantly increasing risk to the system. A second requirement of the DTKM system is to reduce management cost and burden. Traditional key management systems, such as public key infrastructure (PKI), can quickly become difficult to manage at scale; accepting operational risk is often the path chosen to overcome these challenges. The DTKM system is tailored to address the unique properties of both the cyber and physical attributes of EDSs to ensure a strong foundation for implementing secure applications. The following impacts are expected as outcomes of this project: 

* **Automate key management services** – Automating device key management relieves operational burden and increases the appeal of security applications. The DTKM system includes a notification system to alert of expiring or revoked cryptographic material. 
* **Centralize cryptographic policy management** – While distributed operation is crucial to maintaining stable and secure EDSs, distributing control of the system is resource-prohibitive. The DTKM system specifies how the authentication and authorization policies can be managed centrally while still providing distributed operation.
* **Distribute authorization services** – Distributed authorization services makes identity and authorization management for both users and devices more efficient. While the protocol and service will be distributed leveraging a modified Kerberos protocol, centralized policy management will enable per-user and per-device authentication as well as role-based access control (RBAC). 
* **Continuously monitor key management processes** – While the DTKM system is being designed to be secure against attack, centrally-managed key management systems add additional risks. Since key management systems are high value targets, the DTKM system specifies using the Bro platform for secondary monitoring in order to mitigate these risks. 
* **Centralize cryptographic material generation** – A common challenge within EDSs is maintaining the ability for field devices to support necessary levels of cryptographic security. EDS equipment is often designed to last decades; over time, maintaining up-to-date security postures can be difficult. Two areas in particular lack updateability for future security: having the resource capacity to perform advanced cryptography, and having the necessary amount of high entropy data available for performing the number of cryptographic actions. One of the most resource-consuming tasks is the generation of asymmetric keys. Offloading key generation removes this risk by utilizing an updatable platform design to generate large quantities of entropy data.
* **Increase assurance of third party connectivity** – Process control networks often require third party access to equipment both during emergencies and for regular maintenance. The DTKM system allows utilities to enable third party access to equipment through out-of-band processes.

## Guides
### Installation and Configuration
Start here. View the installation guide for how to initially get everything set up.

### Usage
Please view the usage guide once you have everything needed installed and configured. 

### File Structure
Under the Beaglebone Files folder you will find folders containing the code for the wrappers, the ADC and the 61850 applications. 
