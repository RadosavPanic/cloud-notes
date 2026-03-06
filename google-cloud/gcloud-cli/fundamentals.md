# Gcloud

Gcloud is a **CLI (Command Line Interface)** to interact with GC Resources.

GCloud CLI can be used for most services:

- Compute Engine VMs
- Managed Instance Groups
- Databases
- and more

It allows to perform CRUD operations - Create, Read, Update, Delete on existing resources and perform actions like deployments as well.

> [!IMPORTANT]
> **Some GCP Services have specific CLI tools**
>
> - Cloud Storage: `gsutil`
> - Cloud BigQuery: `bq`
> - Cloud Bigtable: `cbt`
> - Kubernetes: `kubectl` (in addition to `Gcloud` which is used to **manage clusters**)

## Using Gcloud

Gcloud is part **Google Cloud SDK** and **it requires Python**.

Also using Gcloud on **Cloud Shell** is an option:

- Managing infrastructure and developing apps from any browser
- It comes Cloud SDK gcloud, Cloud Code, an online code editor and other utilities pre-installed
- Fully authenticated and up-to-date
