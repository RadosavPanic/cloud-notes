# Internal and External IP Addresses

**External (Public)** IP addresses are Internet addressable.

**Internal (Private)** IP addresses are **internal** to a corporate network.

> [!CAUTION]
> You `cannot have` two resources with same public (External) IP address.

> [!NOTE]
> However, two different corporate networks `can have` resources with same internal (private) IP address.

- All **VM instances** are assigned at least one Internal IP address.
- Creation of External IP addresses can be enabled for VM instances.
  - When you stop an VM instance, External IP address `is lost`.
  - Sometimes Google Cloud reuses `the same External IP` on restart.

## Static IP Addresses

How to get a constant External IP Address for a VM instance?

- Assign an Static IP Address to the VM (quick and dirty way)
- Use Load Balancers

> [!NOTE]
>
> - Static IP **can be switched** to another VM instance in same project
> - Static IP **remains attached** even if you stop the instance. You have to manually detach it.

> [!CAUTION]
>
> - You are `billed for` an Static IP when `you are not using it`.
>   - Make sure that you explicitly **release an Static IP** when you are not using it.
