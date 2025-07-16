# Cloud Patterns

Cloud-specific architectural patterns for modern cloud-native applications.

## Available Patterns

### Infrastructure Patterns
- **[Developer Landing Zone](./developer-landing-zone.md)** 🟢
  - Secure, automated developer environment provisioning
  - *Used in: Development Environments, Sandbox Access*

- **[Multi-Tenant SaaS](./multi-tenant-saas.md)** 🟡
  - Scalable multi-tenant application architecture
  - *Evaluation phase*

- **[Disaster Recovery](./disaster-recovery.md)** 🟢
  - Cross-region backup and recovery strategies
  - *Used in: Critical Business Systems*

### Migration Patterns
- **[Strangler Fig](./strangler-fig.md)** 🟢
  - Gradual legacy system replacement
  - *Used in: Legacy Modernization Projects*

- **[Database Migration](./database-migration.md)** 🟢
  - Zero-downtime database migration strategies
  - *Used in: Platform Migrations*

### Cost Optimization Patterns
- **[Reserved Instance Strategy](./reserved-instances.md)** 🟢
  - Optimal cloud resource reservation planning
  - *Used in: All Production Workloads*

- **[Auto-scaling Patterns](./auto-scaling.md)** 🟢
  - Dynamic resource scaling based on demand
  - *Used in: Variable Load Applications*

## Pattern Categories

| Category | Focus Area | Key Patterns |
|----------|------------|--------------|
| **Infrastructure** | Core cloud infrastructure | Landing Zones, Multi-tenancy |
| **Migration** | Legacy modernization | Strangler Fig, Lift-and-Shift |
| **Cost** | Resource optimization | Reserved Instances, Auto-scaling |
| **Security** | Cloud security | Zero Trust, Identity Management |

## Cloud Provider Specific Guidance

### Azure Patterns
- [Azure Landing Zones](./azure-landing-zones.md)
- [Azure DevOps Integration](./azure-devops.md)

### AWS Patterns
- [AWS Well-Architected](./aws-well-architected.md)
- [AWS Control Tower](./aws-control-tower.md)

### Multi-Cloud Patterns
- [Cloud Abstraction Layer](./cloud-abstraction.md)
- [Cross-Cloud Data Sync](./cross-cloud-sync.md)

## Related Documentation
- [Security Patterns](../security-patterns/README.md)
- [Infrastructure Standards](../../standards/infrastructure-standards.md)
- [Cloud Strategy](../../reference-architectures/cloud-strategy.md)

---
[← Back to Patterns](../README.md) | [← Back to Home](../../README.md)
