# Using GPUs in GCE

Using GPUs in Compute Engine VMs is a way to accelerate `math intensive` and `graphics intensive` workloads (etc. for AI/ML).

Adding a GPU to the Virtual Machine:

- Enables high performance for math intensive and graphics intensive workloads
- **Higher cost**
- Use `images with GPU libraries` (Deep Learning) installed

> [!WARNING]
> **RESTRICTIONS**
>
> - `Not supported on all machine types` (etc. on shared-core or memory-optimized machine types)
> - `On host maintenance` can only have the value `"Terminate VM instance"`

Recommend **Availability Policy** for GPUs:

- Automatic restart - `on`
