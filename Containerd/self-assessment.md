# Self-assessment
The Self-assessment is the initial document for projects to begin thinking about the
security of the project, determining gaps in their security, and preparing any security
documentation for their users. This document is ideal for projects currently in the
CNCF **sandbox** as well as projects that are looking to receive a joint assessment and
currently in CNCF **incubation**.

For a detailed guide with step-by-step discussion and examples, check out the free 
Express Learning course provided by Linux Foundation Training & Certification: 
[Security Assessments for Open Source Projects](https://training.linuxfoundation.org/express-learning/security-self-assessments-for-open-source-projects-lfel1005/).

# Self-assessment outline

## Table of contents

* [Metadata](#metadata)
  * [Security links](#security-links)
* [Overview](#overview)
  * [Actors](#actors)
  * [Actions](#actions)
  * [Background](#background)
  * [Goals](#goals)
  * [Non-goals](#non-goals)
* [Self-assessment use](#self-assessment-use)
* [Security functions and features](#security-functions-and-features)
* [Project compliance](#project-compliance)
* [Secure development practices](#secure-development-practices)
* [Security issue resolution](#security-issue-resolution)
* [Appendix](#appendix)

## Metadata

A table at the top for quick reference information, later used for indexing.

|   |  |
| -- | -- |
| Software | A link to the software’s repository.  |
| Security Provider | Yes or No. Is the primary function of the project to support the security of an integrating system?  |
| Languages | languages the project is written in |
| SBOM | Software bill of materials.  Link to the libraries, packages, versions used by the project, may also include direct dependencies. |
| | |

### Security links

Provide the list of links to existing security documentation for the project. You may
use the table below as an example:
| Doc | url |
| -- | -- |
| Security file | https://my.security.file |
| Default and optional configs | https://example.org/config |

## Overview

Containerd is a Cloud Native Computing Foundation (CNCF) Project focused on providing the core functionalities for container orchestration. Specifically architected to focus on modularity and compatibility, this provides a secure and minimal approach making it a great option for integrating into different container systems. 

### Background

#### Introduction:
Containerd, a fundamental tool in the realm of containerization, provides a dependable and standardized approach to managing containers. It is a lightweight yet powerful container runtime, ensuring a consistent and efficient experience.

#### Origins and Evolution:
Originally developed by Docker, Inc. as an integral part of the Docker project, Containerd has evolved with the dynamic container ecosystem. Docker's decision to separate container runtime functionality led to Containerd, an independent project dedicated to container management.

#### Core Features:
**Image and Container Management:**
Containerd oversees the entire lifecycle of containers, handling tasks such as image storage, transfer, execution, and supervision. Its capabilities also extend to other essential operations like pushing, pulling, and managing container images.

**Pluggable Architecture:**
Containerd boasts a modular and adaptable architecture, allowing for the assembly and reassembly of independent components. This flexibility caters to the diverse requirements of container environments.

**Security:**
With a strong emphasis on security, Containerd implements features like user namespaces and seccomp profiles. These measures enhance container isolation, ensuring a robust security posture.

**Compatibility:**
Aligned with the Open Container Initiative (OCI) specifications, Containerd ensures compatibility with other runtimes and tools adhering to the OCI standard. This compatibility facilitates easy transitions between container runtimes supporting OCI.

**CLI and APIs:**
Containerd provides well-defined APIs for programmatic interaction with container runtimes. Additionally, its Command-Line Interface (CLI) allows manual management of containers and images.

**Production Ready:**
Widely adopted in multiple container orchestration platforms and cloud-native environments, Containerd has proven itself as a production-ready solution. Its reliability is evidenced by its integration into various deployments of containerized applications.

**Community and Governance:**
As an open-source project under the Cloud Native Computing Foundation (CNCF), Containerd benefits from a diverse community of contributors. This collaborative approach ensures transparent decision-making, promoting inclusiveness and continuous improvement.

**Conclusion:**
Containerd serves as a crucial foundation in the container ecosystem, providing a dependable and standardized runtime for containers. Its modular architecture, robust features, and strong community support contribute to its widespread adoption in container orchestration platforms and deployments of containerized applications.

### Actors
**1. Containerd Core:**
Role: Serves as the core orchestration engine, managing the execution of container-related actions.
Significance: Defines the fundamental behavior of the container runtime, providing the essential framework for container management.
**2. Container Runtimes:**
Role: Executes containers based on specifications provided by containerd, interacting directly with the underlying operating system.
Significance: Key players responsible for translating container configurations into actual running instances, ensuring compatibility and adherence to standards.
**3. Image Registries:**
Role: Acts as repositories for container images, collaborating with containerd in tasks such as image pulling, pushing, and managing metadata.
Significance: Critical components for image distribution, storage, and retrieval, forming a pivotal part of the containerized ecosystem.
**4. System Administrators:**
Role: Configures, monitors, and maintains containerd in the broader system context, overseeing its integration into the overall infrastructure.
Responsibilities: Involves setup, continuous monitoring, optimization, and troubleshooting of containerd to ensure seamless operation.
**5. Developers/Contributors:**
Role: Actively contributes to the containerd project through codebase enhancements, bug fixes, and feature development.
Responsibilities: Shapes the evolution of containerd, addressing issues, introducing improvements, and ensuring the project's ongoing robustness.
**6. End Users:**
Role: Leverage containerd for deploying, managing, and orchestrating containerized applications.
Interaction: Engage with containerd through various interfaces and tools, contributing to the widespread adoption and integration of containerized solutions.

### Actions
**1. Container Lifecycle Management:**
Description: Orchestrates the complete lifecycle of containers, covering creation, initialization, termination, and removal.
Significance: Acts as the backbone of container orchestration, ensuring the smooth execution of containerized applications throughout their lifecycle.
**2. Image Operations:**
Description: Manages various image-related operations, including pulling images from repositories, pushing images to registries, and handling image metadata.
Significance: Central to image management within the container ecosystem, enabling efficient distribution and storage of container images.
**3. Resource Isolation and Management:**
Description: Enforces robust resource isolation for individual containers, including CPU, memory, and network resources.
Significance: Optimizes resource utilization, preventing interference between containers and ensuring performance isolation.
**4. Network Configuration:**
Description: Configures and manages network settings for containers, facilitating communication and maintaining network isolation.
Significance: Ensures effective container communication while safeguarding against security vulnerabilities through proper network segmentation.
**5. Security Implementation:**
Description: Implements comprehensive security measures within containers, covering access controls, encrypted communication, and permission management.
Significance: Strengthens the overall security posture of containerized applications, mitigating potential vulnerabilities and ensuring secure execution.

### Goals
**1. Component Independence:**
Components should not have tight dependencies on each other, allowing them to be used independently while maintaining a natural flow when used together.
**2. Primitives over Abstractions:**
Containerd should expose primitives to solve problems instead of building high-level abstractions in the API. This allows flexibility for higher-level implementations.
**3. Extensibility:**
Containerd should provide defined extension points for various components, allowing alternative implementations to be swapped. For example, it uses runc as the default runtime but supports other runtimes conforming to the OCI Runtime specification.
**4. Defaults:**
Containerd comes with default implementations for various components, chosen by maintainers. These defaults should only change if better technology emerges.
**5. Scope Clarity:**
The project scope is clearly defined, and any changes require a 100% vote from all maintainers. The whitelist approach ensures that anything not mentioned in scope is considered out of scope.

### Non-goals
**1. Component Tight Coupling:**
Components should not have tight dependencies, promoting independence.
**2. High-Level Abstractions in API:**
Avoid building high-level abstractions in the API, focus on exposing primitives.
**3. Acceptance of Additional Implementations:**
Additional implementations for core components should not be accepted into the core repository and should be developed separately.
**4. Build as a First-Class API:**
Building images is considered a higher-level feature and is out of scope.
**5. Volume Management:**
Volume management for external data is out of scope. The API supports mounts, binds, etc., allowing different volume systems to be built on top.
**6. Logging Persistence:**
Logging persistence is considered out of scope. Clients can handle and persist container STDIO as needed.

## Self-assessment use

This self-assessment is created by the Containerd team to perform an internal analysis of the project's security.  It is not intended to provide a security audit of Containerd, or function as an independent assessment or attestation of Containerd's security health.

This document serves to provide Containerd users with an initial understanding of Containerd's security, where to find existing security documentation, Containerd plans for security, and general overview of Containerd security practices, both for development of Containerd as well as security of Containerd.

This document provides the CNCF TAG-Security with an initial understanding of Containerd to assist in a joint-assessment, necessary for projects under incubation.  Taken together, this document and the joint-assessment serve as a cornerstone for if and when Containerd seeks graduation and is preparing for a security audit.

## Security functions and features

#### Critical
**1. Namespaces**
Namespaces creates more security and efficiency by allowing multiple consumers to use the same containerd without conflicts. It has the benefit of separation of containers and images, while sharing content. 

**2. Capabilities**
Containerd pushes toward a least-privilege process for managing access. This limits kernel capabilities for processes. Other systems with less least-privilege could create vulnerabilities and increase their attack surfaces.

**3. Isolation**
With its capability systems and namespaces, containerd provides industry standard resource isolation, ensuring the resources remain isolated and secured.

**4. Modularity**
Containerd allows people to use different container systems. This gives users of containerd authority over runtimes, but if not properly handled, could lead to severe access

#### Security Relevant
**1. Plug-ins**
Containerd allows external plugins like AppArmor and Seccomp which can decrease the attack surface of the container management. However, this also creates separate challenges not managable directly from a Containerd implementation.

**2. Network Security**
Containerd allows for network isolation, helping lockdown containers with network changes. This prevents unauthorzed communication, but needs to be monitored properly

**3. Trust**
Containerd only stores identical content once, reducing risk of storing multiple copies of vulnerable content, thereby reducing the attack surface. If more things are uploaded, this needs to be monitored as it has a big effect on the attack surface.

## Project compliance
Containerd is not documented as meeting any major security standards except for having bypassed a test in fuzzing. The testing done by Adacompliance deemed that the fuzzing prevention was strong and with further testing was incredibly robust for industry application.

It is reasonable to suggest its minimal framework could support CIS Benchmarks on least privilege and access control policies in ISO. However, there is no public documentation with proof to having matched any of these requirements. 

## Secure development practices

* Development Pipeline.  A description of the testing and assessment processes that
  the software undergoes as it is developed and built. Be sure to include specific
information such as if contributors are required to sign commits, if any container
images immutable and signed, how many reviewers before merging, any automated checks for
vulnerabilities, etc.
* Communication Channels. Reference where you document how to reach your team or
  describe in corresponding section.
  * Internal. How do team members communicate with each other?
  * Inbound. How do users or prospective users communicate with the team?
  * Outbound. How do you communicate with your users? (e.g. flibble-announce@
    mailing list)
* Ecosystem. How does your software fit into the cloud native ecosystem?  (e.g.
  Flibber is integrated with both Flocker and Noodles which covers
virtualization for 80% of cloud users. So, our small number of "users" actually
represents very wide usage across the ecosystem since every virtual instance uses
Flibber encryption by default.)

## Security issue resolution

* Responsible Disclosures Process: The responsible disclosure process for containerd is designed to manage the identification of security issues, incidents, or vulnerabilities, whether discovered internally or externally. If a security issue is found within the project team, it is reported using the same procedures as external reports. External discoveries are encouraged to follow a responsible disclosure process, which involves reporting the issue either on GitHub or via email. GitHub is the primary platform, allowing individuals to navigate to the security tab, access the Advisories tab, and use the "Report a vulnerability" option. Alternatively, an email can be sent to security@containerd.io, including details of the issue and steps to reproduce. Reporters should anticipate an acknowledgment within 24 hours and are advised to contact any committer directly if there's no response.

  * Vulnerability Response Process: The responsibility for responding to a reported vulnerability rests with the committers of containerd. Once a committer confirms the relevance of the reported vulnerability, a draft security advisory is created on GitHub. Reports can be submitted through GitHub or via email to security@containerd.io. Reporters interested in participating in the discussion can provide their GitHub usernames for an invitation. Alternatively, they can opt to receive updates via email. If the vulnerability is accepted, a timeline for developing a patch, public disclosure, and patch release is established. In cases where an embargo period precedes public disclosure, an announcement is sent to the security announce mailing list, detailing the vulnerability scope, patch release date, and public disclosure date. Reporters are expected to engage in the discussion of the timeline and adhere to agreed-upon dates for public disclosure.

* Incident Response: Defined procedures are in place for triaging reported vulnerabilities, assessing their severity and relevance. The confirmation process involves validating the reported vulnerability to determine its authenticity and impact. If the vulnerability is confirmed, the involved parties, including the reporter(s), are notified. A timeline for developing a patch and making updates available is determined. Depending on the embargo period, the vulnerability and patch release details are publicly disclosed using the security announce mailing list. Reporters are expected to comply with agreed-upon dates for public disclosure, ensuring a responsible and coordinated release of information. This process ensures a systematic and transparent approach to handling security issues, promoting responsible disclosure, and achieving timely resolution.

## Appendix

* Known Issues Over Time. List or summarize statistics of past vulnerabilities
  with links. If none have been reported, provide data, if any, about your track
record in catching issues in code review or automated testing.
* [CII Best Practices](https://www.coreinfrastructure.org/programs/best-practices-program/).
  Best Practices. A brief discussion of where the project is at
  with respect to CII best practices and what it would need to
  achieve the badge.
* Case Studies. Provide context for reviewers by detailing 2-3 scenarios of
  real-world use cases.
* Related Projects / Vendors. Reflect on times prospective users have asked
  about the differences between your project and projectX. Reviewers will have
the same question.
