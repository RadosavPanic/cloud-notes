# Gcloud Compute Commands

## Instances

1. `gcloud compute instances list`: Lists all VM instances (running/terminated)
   ```
   NAME: instance-template-weather-vm-with-custom-image-20260303-085324
   ZONE: us-central1-a
   MACHINE_TYPE: e2-medium
   PREEMPTIBLE:
   INTERNAL_IP: 10.128.0.5
   EXTERNAL_IP:
   STATUS: TERMINATED
   ```
2. `gcloud compute instances create instanceName`: Creates an instance with specified name
3. `gcloud compute instances delete instanceName`: Deletes an instance with specified name
4. `gcloud compute instances describe instanceName`: Lists all properties with values for an instance with specified name

## Zones

1. `gcloud compute zones list`: Lists all zones with relevant info

   ```
   NAME: us-east1-b
   REGION: us-east1
   STATUS: UP
   NEXT_MAINTENANCE:
   TURNDOWN_DATE:

   NAME: us-east1-c
   REGION: us-east1
   STATUS: UP
   NEXT_MAINTENANCE:
   TURNDOWN_DATE:
   ```

## Regions

1. `gcloud compute regions list`: Lists all regions with relevant info

   ```
   NAME: europe-north1
   CPUS: 0/200
   DISKS_GB: 0/4096
   ADDRESSES: 0/8
   RESERVED_ADDRESSES: 0/8
   STATUS: UP
   TURNDOWN_DATE:

   NAME: northamerica-south1
   CPUS: 0/72
   DISKS_GB: 0/4096
   ADDRESSES: 0/8
   RESERVED_ADDRESSES: 0/8
   STATUS: UP
   TURNDOWN_DATE:
   ```

## Machine Types

1.  `gcloud compute machine-types list`: Lists all machine-types with relevant info

    ```
    gcloud compute machine-types list \
       --filter="zone=(asia-southeast2-b asia-southeast2-c)" \
       --sort-by=~guestCpus \
       --format="table(name, guestCpus, memoryMb, zone)"
    ```

    ```
    NAME: n4-highmem-80
    ZONE: asia-southeast2-b
    CPUS: 80
    MEMORY_GB: 640.00
    DEPRECATED:

    NAME: n4-standard-16
    ZONE: asia-southeast2-c
    CPUS: 16
    MEMORY_GB: 64.00
    DEPRECATED:
    ```
