# Compute Engine Machine Families

There are several machine families you can choose from when creating a VM instance. Each machine family is further organized into machine series and predefined machine types within each series.

Machine Families for different workloads:

1. **General purpose**: **E2, N2, N2D, N1** → Best price-performance ratio

- Web and application servers
- Small-medium databases
- Dev environments

2. **Memory optimized**: **M2, M1** → Ultra high memory workloads

- Large in-memory databases
- In-memory analytics

3. **Compute Optimized**: **C2** → Compute intensive workloads

- Gaming applications

## Compute Engine Machine Types Example

**Machine name**: e2-standard-2

**VCPUs**: 2

**Memory (GB)**: 8

**Max number of persistent disks (PDs)<sup>2</sup>**: 128

**Max total PD size (TB)**: 257

**Local SSD**: No

**Maximum egress bandwidth (Gbps)<sup>3</sup>**: 4

> [!NOTE]
> In the name e2-standard-2:
>
> - **e2**: Machine Type Family
> - **standard**: Type of workload
> - **2**: Number of CPUs

For example, **e2-standard-4** has 4 vCPUs, **16 GB** of memory and maximum egress bandwith (Gbps)<sup>3</sup> of **8**, which offers an advantage on previous machine type.

## What OS and software is wanted on the instance?

It is decided by choosing the image of OS during instance creation.

Types of images:

- **Public images**: Provided and maintained by Google or Open source communities or third party vendors
- **Custom images**: Created by you for your projects
