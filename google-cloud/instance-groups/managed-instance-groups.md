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
