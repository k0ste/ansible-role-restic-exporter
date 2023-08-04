# ansible-restic-exporter

Role for deploy Prometheus
[restic-exporter](https://github.com/ngosang/restic-exporter)

## Requirements

* Ansible 3.0.0+;

Example configuration
-------------------------

```yaml
restic_exporter:
  # tag of container https://hub.docker.com/r/ngosang/restic-exporter
  # usually 'latest'
  - version: 'latest'
    # enable exporter service or not (docker service will be enabled)
    enable: 'true'
    # restart exporter service or not (docker service will be started)
    restart: 'true'
    # The configuration of exporter
    settings:
# Restic repo password
      - password: '<secret>'
# For example '/backup' if data is local, or `s3:...` if data in Cloud
        repo: 's3:s3.amazonaws.com/bucket_name'
# S3 access key
        access_key: '<access_key>'
# S3 secret key
        secret_key: '<secret_key>'
# Address to listen
        address: "0.0.0.0"
# Port to listen
        port: '8001'
# Refresh interval for the metrics in seconds. Computing the metrics is a
# expensive task, keep this value as high as possible. Default is '60' seconds
        refresh_interval: '60'
# Shutdown exporter on any restic error. Default is Flase (only log error,
# such as network error with Cloud backends)
        exit_on_error: 'false'
# Do not perform restic check operation for performance reasons. Default is
# 'false' (perform restic check)
        no_check: 'true'
# Do not collect per backup statistics for performance reasons. Default is
# 'false' (collect per backup statistics)
        no_stats: 'true'
# Do not collect the number of locks. Default is 'false' (collect the number of
# locks)
        no_locks: "false"
# Include snapshot paths for each backup. The paths are separated by commas.
# Default is 'false' (not collect the paths)
        include_paths: "false"
```
