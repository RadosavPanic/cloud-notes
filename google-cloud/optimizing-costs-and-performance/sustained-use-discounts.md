# Sustained Use discounts in GCP

Whenever making use of the Cloud, we want to keep our costs as low as possible.

> [!IMPORTANT]
> **Sustained use discounts** are `automatic discounts` for running VM instances for significant portion of the billing month.

**Example**: If you use `N1, N2` machine types for more than 25% of a month, you get a 20% to 50% discount on every incremental minute.

> [!NOTE]
>
> - Discount increases with usage (available on google cloud graph)
> - No action required from our side
> - Applicable for instances created by **Google Kubernetes Engine** and **Compute Engine**

> [!WARNING]
> **RESTRICTIONS**
>
> - Does not apply on certain machine types (etc. E2 and A2)
> - Does not apply to VMs created by App Engine flexible and Dataflow
