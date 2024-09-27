# ansible-ssl_exporter

Role for deploy Prometheus [ssl_exporter](//github.com/ribbybibby/ssl_exporter)

## Requirements

* Ansible 3.0.0+;

Example configuration
-------------------------

```yaml
---
ssl_exporter:
  # Install/upgrade exporter package, otherwise binary from Github will
  # be installed
  - install_package: 'true'
  # 'present' (do nothing if package is already installed) or 'latest' (always
  # upgrade to last version)
    package_state: 'latest'
  # version of the exporter in case of Github deployment (not relevant for
  # package deployment): bare value, like '0.8.0' or latest' - the latest
  # release from Github
    version: 'latest'
    # enable exporter service or not
    enable: 'true'
    # restart exporter service or not
    restart: 'true'
  # Exporter startup options
    options:
      # Address to listen on for web interface and telemetry
      - web_listen_address: ':9219'
      # Path under which to expose metrics
        web_metrics_path: '/metrics'
      # Path under which to expose the probe endpoint
        web_probe_path: '/probe'
      # Only log messages with the given severity or above. One of: [debug,
      # info, warn, error]
        log_level: 'info'
      # Output format of log messages. One of: [logfmt, json]
        log_format: 'logfmt'
    # The configuration of ssl_exporter
    settings:
      modules:
        https:
          prober: 'https'
        https_insecure:
          prober: 'https'
          tls_config:
            insecure_skip_verify: true
        tld.domain.com:
          prober: 'https'
          tls_config:
            server_name: 'tld.domain.com'
```
