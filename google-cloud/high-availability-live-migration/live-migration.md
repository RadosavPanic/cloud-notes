# Compute Engine - Live Migration & Availability Policy

When Compute Engine performs periodic infrastructure maintenance it can migrate your VM instances to other hardware without downtime.

## Live migration

> [!NOTE]
>
> - Your running instance is migrated to another host in the same zone
> - **Does not** change any attributes or properties of VM
> - `Supported` for instances with local SSDs
> - `Not supported` for GPUs and preemptible instances

## Important Configuration - Availability Policy

`On host maintenance`: What should happen during periodic infrastructure maintenance?

- Migrate (default): Migrate VM instance to other hardware
- Terminate: Stop the VM instance

`Automatic restart`: Restart VM instances if they are terminated due to non-user-initiated reasons (maintenance event, hardware failure)
