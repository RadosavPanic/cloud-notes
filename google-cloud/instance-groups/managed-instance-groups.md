# Managed Instance Groups (MIG)

**Managed Instance Group** is an `identical set of VMs` created using an instance template.

**Important features**:

- **Maintain** certain number of instances
  - If an instance crashes, MIG launches another instance
- **Detect application failures** using health checks (**Self Healing**)
- Increase and decrease instances based on load (**Auto Scaling**)
- Add **Load Balancer** to distribute load
- Create instances in multiple zones (regional MIGs)
  - Regional MIGs provide higher availability compared to zonal MIGs
- **Release** new application versions without downtime
  - **Rolling updates**: Release new version step by step (gradually). Update a percentage of instances to the new version at a time.
  - **Canary Deployment**: Test new version with a group of instances before releasing it across all instances.

## Creating MIG

**Instance template** is mandatory for creating **Managed Instance Groups** (MIG).

Next is configuring `auto-scaling` to automatically adjust number of instances based on load:

- **Minimum** number of instances
- **Maximum** number of instances
- **Autoscaling metrics**: `CPU Utilization` target or `Load Balancer Utilization` target or Any other metric from `Stack Driver` (Google Cloud provided Monitoring tool)
  - **Cool-down period**: How long to wait before looking at auto scaling metrics
  - **Scale in Controls**: Prevent a sudden drop in number of VM instances (etc. don't scale in by more than 10% or 3 instances)
- **Autohealing**: Configure a Health check with Initial delay
