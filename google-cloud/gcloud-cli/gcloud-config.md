# Gcloud Config Commands

1. `gcloud config list`: Lists all sections and configurations for the current configuration

   **Example:**

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

   **Example:**
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
