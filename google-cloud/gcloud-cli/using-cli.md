# Using Gcloud CLI

Commands available for Gcloud config:

- `get`: Print the value of a GC CLI property
- `list`: List GC CLI properties for the currently active configuration
- `set`: Set a GC CLI property
- `unset`: Unset a GC CLI property

Basic commands that can be used:

1. `gcloud -v`: Lists the version of Gcloud SDK and list of items installed in addition

   Example:

   | Component            | Version       |
   | -------------------- | ------------- |
   | Google Cloud SDK     | 557.0.0       |
   | app-engine-python    | 1.9.118       |
   | beta                 | 2026.02.17    |
   | bq                   | 2.1.28        |
   | bundled-python3-unix | 3.13.10       |
   | cbt                  | 1.25.1        |
   | core                 | 2026.02.17    |
   | gsutil               | 5.35          |
   | istioctl             | 1.20.860      |
   | kpt                  | 1.0.0-beta.60 |
   | kubectl              | 1.33.5        |
   | local-extract        | 1.6.3         |

2. `gcloud init`: Initialize or reinitialize gcloud

   **Example**:

   ```
   Settings from your current configuration [cloudshell-Xnum] are:
   accessibility:
   screen_reader: 'True'
   component_manager:
   disable_update_check: 'True'
   compute:
   gce_metadata_read_timeout_sec: '30'
   core:
   account: **current-email-account**
   disable_usage_reporting: 'False'
   project: **current-project-id**
   universe_domain: googleapis.com
   metrics:
   environment: devshell
   ```

   Next steps:
   - Pick to re-initialize current configuration [cloudshell-x] with new settings or create new configuration
   - Select a google account to be used
   - Select cloud project to use
   - Prompt to configure a default Compute Region and zone (Y/N)
   - Select from the list of available zones in regions, and option 1 is `Do not set default zone`

3. `gcloud config list`: Lists all properties of the active configuration
4. `gcloud config --help` **/** `gcloud config list --help` **/** `gcloud config set --help`
