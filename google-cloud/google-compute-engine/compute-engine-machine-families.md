# Compute Engine Machine Families

There are several machine families you can choose from when creating a VM instance. Each machine family is further organized into machine series and predefined machine types within each series.

Machine Families for different workloads:

1. **General purpose**: <span style="color:#09b878;">**E2, N2, N2D, N1**</span> → Best price-performance ratio

- Web and application servers
- Small-medium databases
- Dev environments

2. **Memory optimized**: <span style="color:#09b878;">**M2, M1**</span> → Ultra high memory workloads

- Large in-memory databases
- In-memory analytics

3. **Compute Optimized**: <span style="color:#09b878;">**C2**</span> → Compute intensive workloads

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

For example, <span style="color:#09b878;">**e2-standard-4**</span> has 4 vCPUs, <span style="color:#09b878;">**16 GB**</span> of memory and maximum egress bandwith (Gbps)<sup>3</sup> of <span style="color:#09b878;">**8**</span>, which offers an advantage on previous machine type.

## What OS and software is wanted on the instance?

It is decided by choosing the image of OS during instance creation.

Types of images:

- **Public images**: Provided and maintained by Google or Open source communities or third party vendors
- **Custom images**: Created by you for your projects
