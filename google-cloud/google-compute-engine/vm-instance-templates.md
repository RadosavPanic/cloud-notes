# Instance templates

With traditional approach of manual creation of VM instance, specifying or confirming VM instance details is needed - image, instance type etc.

**Instance templates** are used to create `VM instances` and `managed instance groups`. They provide a convenient way to create similar instances.

> [!IMPORTANT]
> Once created, they `**cannot** be updated`.
> To make change, copy an existing template and modify it.

**Optional**: Image family can be specified - etc. **debian-9**. Latest non-deprecated version of the family is used.
