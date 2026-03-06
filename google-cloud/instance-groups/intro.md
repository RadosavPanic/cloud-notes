# Instance Groups

To be able to manage multiple VMs, we can use `instance groups`.

> [!NOTE]
>
> - **Instance groups** are group of VM instances **managed as a single entity**.
> - They enable managing group of similar VMs having similar lifecycle as `one unit`.

There are two types of instance groups:

- **Managed**: Group of `identical VMs` created using a template
  - **Features**: Auto scaling, auto healing and managed releases
- **Unmanaged**: Different configuration for VMs in same group
  - Does not offer auto scaling, auto healing and other services
  - Not recommended unless you need different kinds of VMs

Location of instance groups can be `Zonal` or `Regional`.
**Regional is recommended** and gives us higher availability by being able to distribute instances across different zones.
