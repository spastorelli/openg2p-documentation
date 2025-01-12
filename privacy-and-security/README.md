---
icon: lock-keyhole
---

# Privacy and Security

OpenG2P is a robust and versatile platform built upon the Odoo framework, providing governments and organisations with a comprehensive solution for delivering benefits efficiently. As OpenG2P handles sensitive beneficiary information including personally identifiable information (PII), maintaining the highest standards of security is paramount.

## User authentication and access Control

* **Multi-factor Authentication (MFA)**: Building on Odoo's MFA capabilities, OpenG2P allows users to strengthen their authentication process by requiring multiple factors such as passwords, one-time codes, and biometric verification.
* **Role-Based Access Control (RBAC)**: Administrators define roles and permissions within OpenG2P, ensuring authorised personnel have access to specific functionalities and beneficiary data while preventing unauthorised access.
* **User Groups and Access Rules**: OpenG2P builds upon Odoo's user groups and access rules to provide granular control over beneficiary data access, ensuring data confidentiality is maintained.
* **OAuth and OpenID Connect**: Additionally, OpenG2P's implementation of OAuth and OpenID Connect offers the option to seamlessly connect with Identity platforms such as MOSIP (Modular Open Source Identity Platform). This integration empowers OpenG2P to leverage established identity systems, enabling beneficiaries and users to authenticate securely using their MOSIP credentials. By bridging the gap between OpenG2P and MOSIP, this feature enhances security, reduces authentication friction, and fosters a unified and trusted user experience. This also extends the usage of bio-metric and VC (Verifiable Credentials) based authentications.

## Encryption and data protection

* **Data Encryption**: OpenG2P utilizes Odoo's data encryption protocols to secure data transmission between users' browsers and the server, safeguarding beneficiary data during communication.
* **Database Encryption**: Sensitive beneficiary data stored in the database is encrypted using established encryption algorithms, providing an additional layer of protection.
* **Attachment Security**: Files and attachments uploaded to OpenG2P are securely stored in an S3 bucket and accessed only by authorised users, with unauthorised data exposure.
* **PII Encryption:** OpenG2P has a [privacy module](https://github.com/OpenG2P/openg2p-security) for the registry which encrypts all the PII information stored in the database.

Encryption of data is achieved with production-grade Key Manager module. Learn more >>

## Secure input handling

Input security is handled in the following ways:

* Input validation
* Memory safe programming language (Python)
* Type safe programming using Python Pydantic
* ORM capabilities to avoid SQL Injection threats

## Secure deployment

OpenG2P offers support for Kubernetes-based production grade deployment with security features like [Wireguard](https://www.wireguard.com/), [Istio](https://istio.io/), access control, traffic control etc. [Learn more >>](broken-reference/)

## FAQ

<details>

<summary>OpenG2P is an open-source software. How secure is it?</summary>

In general, for any product, security is handled at multiple levels.

* Product security features

We have privacy and security features embedded in our product and we are constantly striving to add more such features. Please refer to the above note.

OpenG2P is built over Oodo ERP which was elected as the best secure open-source ERP by OWASP in 2021. This is because of the extensive work by the community on the underlying platform. OWASP is the largest security reporting system in the world.

OpenG2P has adopted all the best practices of Oodo. OpenG2P has also adopted the GitHub security validation and has been regularly scanned by GitHub for dependency security.

* Deployment of secure infrastructure

While deployment infrastructure is a choice of the implementer/system integrator we offer secure [production-grade deployment reference architecture](../deployment/) for implementors. This secure infra comprising of Kubernetes, Wireguard, Istio etc offers a high level of data and access security.

* Security policies and processes

OpenG2P team can help review security policies defined by the government/system Integrator. \\

</details>
