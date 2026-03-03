# Custom images

Usually, installing OS patches and software at launch of VM instances increases boot up time.

Solution for this is creation of **custom image** with OS patches and software pre-installed.

Example way of creating custom image is:

1. Create an instance
2. Create a custom image out of that instance
3. Create further instances using that custom image

> [!NOTE]
> Custom image can be created from `an instance`, `a persistent disk`, `a snapshot`, `another image`, or a `file in Cloud Storage`.

Custom image can be shared across projects.

- Google Cloud also provides a feature to **deprecate old images (& specify replacement image)**.
- **Hardening an image** - Customize images to your corporate security standards.

> [!IMPORTANT]
>
> - Prefer using Custom Image to Startup script (startup scripts include boot up time)
> - **Preferred**: creating custom image and using it in an instance template
> - A machine image contains a VM’s properties, metadata, permissions, and data from all its attached disks. You can use a machine image to create, backup, or restore a VM.
