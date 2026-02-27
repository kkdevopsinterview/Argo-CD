# 21. How does Argo CD ensure cluster state matches Git state?

Argo CD continuously compares two states:

**Desired state → defined in Git**

**Live state → running inside Kubernetes cluster**

The **Application Controller** periodically checks for differences
between them. If a difference is detected, the application is marked
**OutOfSync**.

If **auto-sync** is enabled, Argo CD automatically applies changes to
make the cluster match Git. If not, it waits for manual approval.

This constant **reconciliation loop** ensures that the cluster always
reflects what is declared in Git.

This mechanism is the core principle of **GitOps** --- Git defines
truth, and Argo CD enforces it.

## Real-World Example

Someone manually scales a deployment in the cluster. Argo CD detects
**drift** and restores the replica count defined in Git.

## Interview Line

"Argo CD enforces Git as the source of truth through continuous
reconciliation."

------------------------------------------------------------------------

# 22. What are sync waves in Argo CD?

**Sync waves** allow controlling the order in which Kubernetes resources
are deployed during **synchronization**.

Some resources must be created before others. For example:

-   CRDs before Custom Resources
-   Database before application
-   Namespace before deployments

Sync waves assign **numeric values** to resources, and Argo CD applies
them in order.

This ensures proper **dependency handling** during deployment.

## Real-World Example

Deploying database first, then backend, then frontend using defined sync
waves.

## Interview Line

"Sync waves control deployment order of resources."

------------------------------------------------------------------------

# 23. What are hooks in Argo CD?

**Hooks** are special Kubernetes resources that run at specific stages
of the **sync process**.

They allow performing actions:

-   before deployment
-   after deployment
-   during rollback

Hooks are useful for:

-   database migrations
-   validation checks
-   cleanup tasks

They extend deployment logic beyond simple resource application.

## Real-World Example

Running database migration job before application update.

## Interview Line

"Hooks allow custom actions during deployment lifecycle."

------------------------------------------------------------------------

# 24. What is multi-cluster management in Argo CD?

Argo CD can manage multiple **Kubernetes clusters** from a single
control plane.

It stores **cluster credentials** and communicates with remote clusters
using **Kubernetes APIs**.

This enables centralized **GitOps management** across:

-   development
-   staging
-   production
-   regional clusters

It simplifies large-scale Kubernetes operations.

## Real-World Example

Single Argo CD instance managing clusters across multiple regions.

## Interview Line

"Argo CD supports centralized GitOps across multiple clusters."

------------------------------------------------------------------------

# 25. How do you secure Argo CD?

Securing Argo CD involves multiple layers:

-   enabling authentication (OIDC, SSO)
-   configuring RBAC policies
-   restricting network access
-   using TLS encryption
-   limiting cluster access permissions

Since Argo CD controls deployments, **security is critical**.

Role-based access ensures only authorized users can deploy or modify
applications.

## Real-World Example

Using SSO integration so only DevOps team can deploy to production.

## Interview Line

"Argo CD security relies on authentication, RBAC, and network
protection."

------------------------------------------------------------------------

# 26. How does Argo CD handle secrets?

Argo CD does not directly manage secrets securely in Git. Instead, it
integrates with **secret management tools** like:

-   Sealed Secrets
-   External Secrets
-   Vault

Secrets are **encrypted before being stored in Git**.

This ensures Git remains the source of truth without exposing sensitive
data.

Using proper secret management is essential for production environments.

## Real-World Example

Using Sealed Secrets to encrypt Kubernetes secrets stored in Git.

## Interview Line

"Argo CD integrates with secret management tools to secure sensitive
data."

------------------------------------------------------------------------

# 27. What is RBAC in Argo CD?

**RBAC (Role-Based Access Control)** controls user permissions inside
Argo CD.

It defines:

-   who can view applications
-   who can sync
-   who can modify configurations
-   who can access specific projects

RBAC ensures **separation of responsibilities** and prevents
unauthorized changes.

In enterprise environments, RBAC is mandatory.

## Real-World Example

Developers can deploy to dev but only DevOps can deploy to production.

## Interview Line

"RBAC controls deployment permissions in Argo CD."

------------------------------------------------------------------------

# 28. What challenges have you faced using Argo CD in production?

Common challenges include:

-   managing large number of applications
-   handling secret security
-   dealing with sync conflicts
-   scaling for multiple clusters
-   managing drift properly

Proper **Git structure** and **naming conventions** are critical.

Also, monitoring Argo CD health is important to ensure reliable
deployments.

Production use requires disciplined **Git workflows**.

## Real-World Example

Application failing to sync due to missing CRD dependencies.

## Interview Line

"Production GitOps requires structured repositories and strong
governance."

------------------------------------------------------------------------

# 29. How do you troubleshoot a failed sync?

Troubleshooting steps include:

-   checking Argo CD UI for error messages
-   reviewing application events
-   verifying manifest syntax
-   checking cluster permissions
-   ensuring dependencies exist

Logs from **Application Controller** provide detailed error information.

Most failures are due to **misconfiguration** or **permission issues**.

Systematic debugging resolves sync failures quickly.

## Real-World Example

Deployment failing due to missing namespace or incorrect Helm values.

## Interview Line

"Failed sync troubleshooting involves checking logs, permissions, and
manifests."

------------------------------------------------------------------------

# 30. How would you design a GitOps workflow using Argo CD in production?

A production **GitOps workflow** includes:

1 Separate repositories for application code and deployment manifests\
2 Branch strategy for dev, staging, and production\
3 Pull request approval before merge\
4 Argo CD auto-sync for lower environments\
5 Manual approval for production\
6 Secret management integration\
7 Monitoring and alerting

This ensures controlled, auditable, and automated deployments.

Git becomes the **single source of truth**.

The workflow improves **reliability**, **transparency**, and **rollback
capability**.

## Real-World Example

Developer commits update → PR approved → Argo CD deploys automatically →
monitoring verifies health.

## Interview Line

"A production GitOps workflow uses Git as the control plane and Argo CD
as the deployment engine."
