FROM vault:0.6.1

MAINTAINER nocsi <l@nocsi.com>

LABEL vendor="HashiCorp" \
              com.hashicorp.vault.version="0.6.1" \
              com.hashicorp.vault.release-date="2016-08-22"

## Expose the config & tls volumes
              VOLUME ["/vault/config", "/vault/tls"]
