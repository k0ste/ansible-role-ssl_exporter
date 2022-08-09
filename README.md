# ansible-ssl_exporter

Role for deploy Prometheus [ssl_exporter](//github.com/ribbybibby/ssl_exporter)

## Requirements

* Ansible 3.0.0+;

Example configuration
-------------------------

```yaml
---
ssl_exporter:
  # version of the exporter:
  # bare value, like '2.3.2'
  # 'latest' - the latest release from Github
  - version: 'latest'
    # enable exporter service or not
    enable: 'true'
    # restart exporter service or not
    restart: 'true'
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
