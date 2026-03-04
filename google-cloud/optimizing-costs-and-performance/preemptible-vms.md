# Preemptible VM

> [!IMPORTANT]
>
> - Preemptible VM is a short-lived VM and **cheaper up to 80%** than regular compute instances.
>   - It can be stopped by GCP anytime (preempted) within 24 hours
>   - Instances get 30 second warning (to save anything they want to save)

> [!TIP]
> **Use Preempt VMs if:**
>
> - Your applications are fault tolerant
> - You are very cost sensitive
> - Your workload is **not immediate**
>   **Example**: Non immediate batch processing jobs

> [!WARNING]
> **RESTRICTIONS**
>
> - Not always available
> - No SLA and **cannot be migrated** to regular VMs
> - No automatic restarts
> - Free tier credits not applicable

## Stop VMs

Spot VMs are the latest version of preemtible VMs.

Spot VMs `do not have maximum runtime` like Preemptible VMs do with 24 hours.

Other features are similar to traditional preemptible VMs:

- May be reclaimed at any time with 30-second notice
- Not always available
- **Dynamic Pricing**: 60 - 91% discount compared to on-demand VMs
- Free Tier credits not applicable
