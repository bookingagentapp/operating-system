# Infrastructure

Infrastructure patterns, deployment processes, and operational procedures.

## Overview

This section documents how the application is deployed, configured, and operated in production environments.

## Architecture

- [[infra/multi-tenant-database]] - Database architecture and provisioning
- [[infra/tenant-provisioning]] - New tenant setup process
- [[infra/connection-management]] - Database connection switching

## Storage

- [[infra/file-storage]] - S3-compatible storage configuration
- [[infra/image-processing]] - Context-aware image processing
- [[infra/backup-strategy]] - Data backup and recovery

## Jobs & Queues

- [[infra/queue-architecture]] - Multi-tenant job processing
- [[infra/job-isolation]] - Tenant-specific queue management
- [[infra/background-jobs]] - Long-running task patterns

## Monitoring

- [[infra/logging]] - Application logging patterns
- [[infra/error-tracking]] - Error monitoring and alerts
- [[infra/performance-monitoring]] - Performance metrics

## Security

- [[infra/tenant-isolation]] - Data isolation guarantees
- [[infra/api-security]] - API authentication and rate limiting
- [[infra/file-permissions]] - File access control

## Deployment

- [[infra/deployment-process]] - Release workflow
- [[infra/environment-config]] - Environment-specific configuration
- [[infra/docker-setup]] - Container configuration

## Related

- See [[concepts/multi-tenancy]] for architectural patterns
- See `/docs/OPERATIONS/` for detailed procedures
- See `/docs/ADMIN/` for administrative tasks
