# 1. What is Argo CD?

**Argo CD** is a **declarative GitOps continuous delivery tool**
designed specifically for **Kubernetes**.

It automatically deploys applications into Kubernetes clusters by
continuously monitoring a **Git repository**. The idea is simple: **Git
becomes the single source of truth** for infrastructure and application
configuration.

Whenever changes are made to **Kubernetes manifests** or **Helm charts**
in Git, Argo CD detects those changes and synchronizes them with the
cluster.

Unlike traditional CI/CD tools that push changes to clusters, Argo CD
pulls changes from Git and ensures the **cluster state matches the
desired state** defined in Git.

It provides:

-   automated deployments
-   drift detection
-   rollback capability
-   UI for visibility

## Real-World Example

A developer updates a deployment YAML in Git. Argo CD automatically
applies that change to the Kubernetes cluster.

## Interview Line

"Argo CD is a GitOps-based continuous delivery tool for Kubernetes."

------------------------------------------------------------------------

# 2. What is GitOps and how does Argo CD implement it?

**GitOps** is a practice where **Git repositories act as the single
source of truth** for infrastructure and application configuration.

Instead of manually applying changes to clusters, all changes are
committed to Git. A **GitOps tool** continuously monitors the repository
and ensures the cluster reflects what is defined there.

Argo CD implements GitOps by:

-   monitoring Git repositories
-   detecting changes
-   syncing cluster state with Git state
-   detecting drift

This approach improves **auditability**, **rollback capability**, and
**operational consistency**.

## Real-World Example

All Kubernetes deployment changes are made through pull requests, and
Argo CD applies them automatically after approval.

## Interview Line

"GitOps means Git is the source of truth, and Argo CD enforces that
truth in the cluster."

------------------------------------------------------------------------

# 3. Why is Argo CD used in Kubernetes environments?

Kubernetes environments are **dynamic and declarative**. Argo CD fits
perfectly because it manages Kubernetes resources declaratively through
Git.

It provides:

-   automated synchronization
-   environment consistency
-   self-healing
-   visual deployment tracking
-   rollback support

In complex **microservices systems**, managing manual deployments
becomes error-prone. Argo CD reduces **operational risk**.

## Real-World Example

Managing multiple microservices deployments across dev, staging, and
production clusters.

## Interview Line

"Argo CD simplifies Kubernetes deployments using Git-based automation."

------------------------------------------------------------------------

# 4. How does Argo CD differ from traditional CI/CD tools?

Traditional CI/CD tools like Jenkins push changes to clusters after
pipeline execution.

Argo CD follows a **pull-based model**. It continuously watches Git and
pulls changes into the cluster.

Key differences:

-   CI tools handle build and test
-   Argo CD handles deployment
-   CI pushes, Argo CD pulls
-   Argo CD provides drift detection

Argo CD focuses purely on **Kubernetes deployment automation**.

## Real-World Example

CI builds Docker image, Argo CD deploys it via updated manifest in Git.

## Interview Line

"CI builds artifacts; Argo CD deploys them via GitOps."

------------------------------------------------------------------------

# 5. What are the main components of Argo CD?

Argo CD has several **core components**:

-   API Server -- exposes UI and API
-   Application Controller -- monitors and syncs applications
-   Repo Server -- fetches and renders Git manifests
-   Redis -- caching layer

These components work together to monitor Git, compare cluster state,
and apply changes.

Understanding architecture helps in **troubleshooting and scaling**.

## Real-World Example

Repo Server pulls Helm chart, Application Controller syncs it to
cluster.

## Interview Line

"Argo CD components coordinate Git monitoring and cluster
synchronization."

------------------------------------------------------------------------

# 6. What is an Argo CD Application?

An **Application** in Argo CD represents a **Kubernetes application
deployment** defined in Git.

It contains:

-   source repository
-   target cluster
-   target namespace
-   path to manifests

The Application object tells Argo CD what to deploy and where.

Each microservice usually has its own Argo CD Application.

## Real-World Example

One Application per microservice deployment.

## Interview Line

"An Argo CD Application defines what to deploy from Git to a cluster."

------------------------------------------------------------------------

# 7. How does Argo CD detect changes in Git?

Argo CD periodically **polls Git repositories** for changes.

It checks **commit differences** between current cluster state and
desired Git state.

If a difference is detected, Argo CD marks the application as
**OutOfSync**.

It can either wait for manual sync or automatically apply changes if
**auto-sync** is enabled.

This continuous comparison ensures alignment between Git and cluster.

## Real-World Example

New deployment version committed triggers automatic cluster update.

## Interview Line

"Argo CD continuously compares Git state with cluster state."

------------------------------------------------------------------------

# 8. What is declarative deployment in Argo CD?

**Declarative deployment** means defining desired system state in
configuration files instead of writing procedural commands.

In Argo CD, **Kubernetes manifests** define the desired state.

Argo CD ensures the cluster always matches what is declared in Git.

Declarative systems improve **predictability and consistency**.

## Real-World Example

Specifying desired replica count in YAML and letting Argo CD enforce it.

## Interview Line

"Declarative deployment defines desired state; Argo CD enforces it."

------------------------------------------------------------------------

# 9. What is synchronization in Argo CD?

**Synchronization** is the process of making the **cluster state match
the desired state** defined in Git.

When Argo CD detects differences, it applies required changes during
sync.

Sync ensures:

-   resource creation
-   updates
-   deletions

It maintains **configuration consistency**.

## Real-World Example

Updating image tag in Git and syncing to update running Pods.

## Interview Line

"Sync aligns cluster state with Git state."

------------------------------------------------------------------------

# 10. What is the difference between manual sync and auto-sync?

**Manual sync** requires a user to trigger synchronization when
differences are detected.

**Auto-sync** automatically applies changes whenever Git state changes.

Manual sync provides control and validation.\
Auto-sync provides automation and faster deployments.

Choosing between them depends on environment sensitivity.

## Real-World Example

Auto-sync enabled in dev, manual sync in production.

## Interview Line

"Manual sync requires approval; auto-sync applies changes
automatically."
