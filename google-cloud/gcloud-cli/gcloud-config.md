# Gcloud Config Commands

## Basic commands

1. `gcloud config list`: Lists all sections and configurations for the current configuration

   ```
   [accessibility]
   screen_reader = True
   [component_manager]
   disable_update_check = True
   [compute]
   gce_metadata_read_timeout_sec = 30
   [core]
   account = **current-email-account**
   disable_usage_reporting = False
   project = **current-project-id**
   universe_domain = googleapis.com
   [metrics]
   environment = devshell
   ```

2. `gcloud config list propertyName`: Lists property name and value. This is available only for `core` section, for other sections we must use `sectionName/propertyName` to list.
   - **account@cloudshell:~ (project-id) $** `gcloud config list account`

     ```
     [core]
     account = example@gmail.com
     ```

   - **account@cloudshell:~ (project-id) $** `gcloud config list core/account`

     ```
     [core]
     account = example@gmail.com
     ```

   - **account@cloudshell:~ (project-id) $** `gcloud config list accessibility/screen_reader`

     ```
     [accessibility]
     screen_reader = True
     ```

3. `gcloud config set sectionName/propertName value`: Sets the specified property in your active configuration.
4. `gcloud config unset`: Opposite of set.

## Managing multiple configurations

1. `gcloud config configurations list`: Lists all configurations available

   ```
   NAME: cloudshell-Xnum
   IS_ACTIVE: False
   ACCOUNT:
   PROJECT: **current-project-id**
   COMPUTE_DEFAULT_ZONE:
   COMPUTE_DEFAULT_REGION:

   NAME: first-config
   IS_ACTIVE: True
   ACCOUNT: **email-account**
   PROJECT: **project-id**
   COMPUTE_DEFAULT_ZONE: us-east1-b
   COMPUTE_DEFAULT_REGION: us-east1

   NAME: second-config
   IS_ACTIVE: False
   ACCOUNT: **email-account**
   PROJECT: **project-id**
   COMPUTE_DEFAULT_ZONE: us-west1-a
   COMPUTE_DEFAULT_REGION: us-west1
   ```

2. `gcloud config configurations describe configName`: Describes specified configuration

   ```
   is_active: false
   name: second-config
   properties:
    compute:
      region: us-west1
      zone: us-west1-a
    core:
      account: **email-account**
      project: **project-id**
   ```

3. `gcloud config configurations activate configName`: Activates specified configuration
4. `gcloud config configurations create configName`: Creates and activates configuration with specified configuration name
5. `gcloud config configurations delete configName`: Deletes specified configuration
