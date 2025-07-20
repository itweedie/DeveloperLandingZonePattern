# Developer Landing Zone Architectural Pattern

| Attribute                  | Value                          |
|---------------------------|---------------------------------|
| Pattern Name              | Developer Landing Zone Pattern |
| Architecture Continuum    | Common Systems Architecture     |
| Domain                    | Identity & Access Management    |
| Reusability               | High                            |
| Applicable Layers         | Application, Technology         |




## Intent
Provide a secure, automated, and reusable approach for onboarding and offboarding developers into isolated landing zones within a dedicated Azure tenant, leveraging identity governance, access packages, and automation.

## Context
- Organizations require isolated environments for development activities, often in separate Azure tenants.
- Access must be controlled, auditable, and limited to authorized corporate users.
- Developer onboarding/offboarding should be automated to reduce manual effort and risk.

## Principles
- **Least Privilege**: Users are granted only the access necessary for their role and tasks.
- **Separation of Duties**: Administrative and user roles are clearly separated to reduce risk.
- **Automated Governance**: All onboarding and offboarding actions are automated and auditable.
- **Scalability**: The pattern supports growth in users, landing zones, and resources without redesign.
- **Interoperability**: Integrates with existing corporate identity and resource management systems.
- **Resilience**: Handles errors and exceptions gracefully, ensuring consistent state and notifications.
- **Compliance**: Aligns with organizational and regulatory requirements for identity and access management.
- **Security**: Only authorized users from the corporate tenant should access developer resources.
- **Automation**: Minimize manual provisioning and deprovisioning steps.
- **Auditability**: All access and changes must be tracked.
- **Scalability**: The pattern should support multiple landing zones and users.
- **User Experience**: Developers should have a seamless experience accessing resources.

### Architecture Layers Diagram
![Architecture Layers Diagram](https://www.plantuml.com/plantuml/png/hPD1Rvmm48Nl_8fH3hqH8aNjeOSgAzfKI4s9IczH3XCpi5Rm6Dd3haZL_rx045Xj3v7Q6_xy_DvunjnuGIUTQIB_hBb5XmOQpIHzIs2TxErcesmrN5zTRKYBwXbhAgHl21mfGQuRYgAPmyMjxRX4qPPXvzHU2odf75q0UhZTmQy8u67tCX3umk8Gii-FuzQ40dbus8kq_cEID8IEBurMpdfRoQMo9Y6EEv_WA4zGYJvGNEgn4ElwvF5njBzR3i3rX_UJ-ztmiV4z7ez_TNrbyQ0FNlVsI0xk6vJAEZEPJMWX6zTsvEtCJ_tdmhAIMBJqyDKUo36o8YW4kKHN-ibxKQo2Vsb7_Ueo5l1xCwNK6cCPYjuB6Ny-gRHOHgKK-U7EuM0eCh05_QS2ftitP8WbDiXOXq-Sik9s3Wjz_46TnwU68ESdYwxKN2TvLItVGxKYv3XKkseMVDA9ZClEY-lFUv3DBLWKST6IqfLMa5hJDdgQJduWrs0VebQ-u9EetDN8-cNwELQpiznywNqwn5e3nHuTtLlDCeK4ki8tzT-FydQKpqznZU_46XI2RxOEqvt1i7wBTNZsCSwdPlllQCP1f9OFnEDzFRo3dyJ8icqZLpg41lshFCpeTWTnQOySVnhVOvGMwphRHTcwoeVTw8Q6EPdc3m00)


```plantuml
@startuml
skinparam linetype ortho
skinparam dpi 300
skinparam packageStyle rectangle

package "Foundation Architecture" as FA {
  [Azure Entra ID] as AzureEntra [[https://learn.microsoft.com/en-us/azure/active-directory/]]
  [Microsoft 365] as M365 [[https://www.microsoft.com/en-us/microsoft-365]]
  [Power Platform] as PowerPlatform [[https://powerplatform.microsoft.com/]]
  [Identity Governance Standards] as IdentityGovernance [[https://learn.microsoft.com/en-us/azure/active-directory/governance/]]
}

package "Common Systems Architecture" as CSA {
  [Access Packages] as AccessPackages [[https://learn.microsoft.com/en-us/azure/active-directory/governance/entitlement-management-access-packages]]
  [Reusable Onboarding/Offboarding Patterns] as OnboardingPatterns
}

package "Industry Architecture" as IA {
  [Industry-Specific Compliance Overlays] as ComplianceOverlays
}

package "Organization-Specific Architecture" as OSA {
  [Custom SharePoint] as CustomSharePoint [[https://learn.microsoft.com/en-us/sharepoint/]]
  [Specific Automate Log] as AutomateLog [[https://learn.microsoft.com/en-us/power-automate/]]
  [Naming Conventions & Tenant-Specific Config] as NamingConventions
}

FA -down-> CSA
CSA -down-> IA
IA -down-> OSA

@enduml
```


## Pattern

### Key Components

1. **Developer Tenant**
   - Azure Entra P2 for advanced identity governance and access packages.
   - Dedicated for developer resources.

2. **Access Packages**
   - Restrict access to users from the corporate tenant.
   - Approval workflow (manual or automatic).
   - Assign users to Office 365 Group and SharePoint Communication Site.

3. **Office 365 Group**
   - Membership managed by Access Package assignment.
   - Triggers Power Automate flows on add/remove.

4. **SharePoint Communication Site**
   - Hosts resources and documentation for developers.
   - Accessible with corporate credentials via B2B collaboration.

5. **Power Automate Flows**
   - Onboarding: Create/enable DLZ user, email credentials, add to security group.
   - Offboarding: Remove DLZ user from security group, disable if not in other groups, notify user.

6. **Security Groups**
   - Control access to developer landing zone resources.
   - Managed by Power Automate flows.

### Onboarding Flow
```mermaid
flowchart TD
    A[Corporate User Requests Access] --> B[Access Package in Developer Tenant]
    B --> C[Approval Workflow]
    C --> D[User Added to Office 365 Group]
    D --> E[Power Automate Flow Triggered]
    E --> F{DLZ User Exists?}
    F -- No --> G[Create DLZ User]
    F -- Yes --> H[Enable DLZ User]
    G --> I[Email Credentials to Corporate User]
    H --> I
    I --> J[Add DLZ User to Security Group]
    J --> K[Access Developer Resources]
    D --> L[Add User to SharePoint Site]
    L --> K
    K --> M[User Accesses Resources]
```

### Removal/Offboarding Flow
```mermaid
flowchart TD
    N[User Removed from Access Package] --> O[Removed from Office 365 Group]
    O --> P[Power Automate Flow]
    P --> Q[Remove DLZ User from Security Group]
    Q --> R{DLZ User in Other Security Groups?}
    R -- No --> S[Disable DLZ User & Notify]
    R -- Yes --> T[No Action]
```



## Consequences
- **Pros:**
  - Automated, auditable onboarding/offboarding.
  - Secure access for corporate users only.
  - Scalable for multiple landing zones.
  - Reduces manual errors and administrative overhead.
- **Cons:**
  - Requires Azure Entra P2 licensing.
  - Initial setup of automation and access packages can be complex.

## Configuration Options

| Component                | Option/Setting                                  | Description                                    |
|--------------------------|-------------------------------------------------|------------------------------------------------|
| Access Package           | External User Restriction                       | Only allow corporate tenant users              |
| Access Package           | Approval Workflow                               | Manual or automatic approval                   |
| Access Package           | Assignment Duration                             | Time-bound or permanent                        |
| Office 365 Group         | Membership Type                                 | Dynamic or static                              |
| SharePoint Site          | Permissions                                     | Read/Write/Owner roles                         |
| Power Automate           | Notification Settings                           | Email templates, recipients                    |
| Security Group           | Resource Assignment                             | Linked to landing zone resources               |

## References
- [Azure AD Entitlement Management](https://learn.microsoft.com/en-us/azure/active-directory/governance/entitlement-management-access-packages)
- [Microsoft 365 Groups](https://learn.microsoft.com/en-us/microsoft-365/groups/overview)
- [SharePoint Communication Sites](https://learn.microsoft.com/en-us/sharepoint/communication-sites)
- [Power Automate](https://learn.microsoft.com/en-us/power-automate/)
- [Azure AD Security Groups](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal)

## Summary
This architectural pattern enables secure, automated onboarding and offboarding of developers into isolated landing zones, leveraging Azure Entra P2, Access Packages, Office 365 Groups, SharePoint, and Power Automate. It is designed for reusability, scalability, and compliance in enterprise environments.
