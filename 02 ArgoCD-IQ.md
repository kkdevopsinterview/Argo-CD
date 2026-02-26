# 11. What is the Argo CD architecture?

**Argo CD** follows a **controller-based architecture** designed
specifically for **Kubernetes**.

It consists of multiple **core components** working together:

-   **API Server** -- exposes REST API and UI
-   **Application Controller** -- continuously monitors applications and
    performs sync
-   **Repo Server** -- fetches and renders manifests from Git
    repositories
-   **Redis** -- caching and state storage

The **Application Controller** compares **desired state (from Git)**
with **actual cluster state**. If differences exist, it triggers
**synchronization**.

The **Repo Server** is responsible for handling **Helm charts**,
**Kustomize**, or plain YAML rendering before deployment.

This architecture makes Argo CD **scalable and modular**.

## Real-World Example

Repo Server fetches Helm chart → Controller compares → API Server shows
status in UI.

## Interview Line

"Argo CD architecture separates Git rendering, state comparison, and
synchronization."

------------------------------------------------------------------------

# 12. How does Argo CD connect to Kubernetes clusters?

Argo CD connects to **Kubernetes clusters** using **Kubernetes API
credentials**.

By default, it manages the cluster where it is installed, but it can
also manage **external clusters**.

It stores **cluster credentials securely** and communicates using
**Kubernetes APIs** to apply manifests.

This allows centralized **GitOps management** across multiple clusters.

Cluster access is usually controlled through **service accounts** and
**RBAC**.

## Real-World Example

One central Argo CD instance managing staging and production clusters.

## Interview Line

"Argo CD uses Kubernetes API access to manage clusters."

------------------------------------------------------------------------

# 13. What is the role of the Argo CD API Server?

The **API Server** acts as the main interface for users and external
tools.

It provides:

-   Web UI
-   CLI access
-   REST API

Through the API Server, users can:

-   view application status
-   trigger sync
-   manage projects
-   configure access control

It also **authenticates users** and enforces **RBAC policies**.

## Real-World Example

Using Argo CD UI to manually sync an application.

## Interview Line

"The API Server provides UI and access control for Argo CD."

------------------------------------------------------------------------

# 14. What is the Application Controller in Argo CD?

The **Application Controller** is the heart of Argo CD.

It continuously monitors **Git repositories** and compares them with the
**live cluster state**.

If differences are found, it marks the application as **OutOfSync** and
optionally triggers **synchronization**.

It also performs **health checks** and manages **rollbacks**.

Without the controller, Argo CD would not detect **drift** or enforce
**desired state**.

## Real-World Example

Controller detecting that replica count was changed manually and
correcting it.

## Interview Line

"The Application Controller enforces Git as the source of truth."

------------------------------------------------------------------------

# 15. What is the Repo Server?

The **Repo Server** is responsible for fetching application manifests
from **Git repositories**.

It supports:

-   plain YAML
-   Helm charts
-   Kustomize

The Repo Server renders manifests into final **Kubernetes resources**
before the controller applies them.

It ensures deployment configurations are processed correctly.

## Real-World Example

Repo Server rendering Helm chart templates before deployment.

## Interview Line

"Repo Server fetches and renders manifests from Git."

------------------------------------------------------------------------

# 16. What is drift detection in Argo CD?

**Drift detection** means identifying when the **live cluster state**
differs from the **desired state defined in Git**.

If someone manually changes a resource in the cluster, Argo CD detects
the difference.

It marks the application as **OutOfSync**.

This helps maintain **configuration consistency** and prevents
unauthorized changes.

Drift detection is a key feature of **GitOps**.

## Real-World Example

Manual change to replica count corrected automatically.

## Interview Line

"Drift detection ensures cluster state matches Git state."

------------------------------------------------------------------------

# 17. How does Argo CD handle rollbacks?

Argo CD maintains **application deployment history**.

If a new deployment causes issues, users can roll back to a **previous
Git revision**.

Rollback restores cluster state to a previously working version.

Because Git stores history, rollback becomes simple and traceable.

This improves **reliability** and **recovery speed**.

## Real-World Example

Rolling back to previous stable version after faulty deployment.

## Interview Line

"Rollback in Argo CD means reverting to a previous Git commit."

------------------------------------------------------------------------

# 18. What is health status in Argo CD?

**Health status** shows whether deployed resources are functioning
correctly.

Argo CD evaluates resource health using **Kubernetes status
information**.

Health states include:

-   Healthy
-   Progressing
-   Degraded
-   Missing

Health monitoring helps teams detect **application failures** early.

## Real-World Example

Deployment marked degraded due to pod crash.

## Interview Line

"Health status reflects real-time resource condition."

------------------------------------------------------------------------

# 19. How do you manage multiple environments using Argo CD?

Multiple environments are managed by:

-   separate Git branches
-   separate directories
-   separate Argo CD Applications
-   different namespaces or clusters

Each environment points to its specific configuration path.

This allows consistent but isolated deployments.

GitOps ensures all environments follow the same deployment model.

## Real-World Example

Dev and production using different directories in same repository.

## Interview Line

"Argo CD manages multi-environment deployments through Git structure."

------------------------------------------------------------------------

# 20. How do you integrate Helm with Argo CD?

Argo CD natively supports **Helm**.

Instead of installing Helm manually, Argo CD pulls **Helm charts** from
Git or Helm repositories and renders them.

Values files can be customized per environment.

This allows combining **GitOps workflow** with **Helm templating**.

It simplifies managing complex Kubernetes applications.

## Real-World Example

Deploying application using Helm chart stored in Git.

## Interview Line

"Argo CD renders and deploys Helm charts declaratively."
