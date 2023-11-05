# Ansible Role: ACME.sh

This role installs the Shell script `ACME.sh` on the system in question. `ACME.sh` is a utility managing the
issuance, renewal and management of TLS certificates with public free Certificate Authorities like **ZeroSSL** or
**Let's Encrypt**.

This role installs the utility itself, issues certificates according to the role variables and installs those for
use by other applications. Installation for Nginx and Apache is supported. Furthermore the role also configured
renewal of the certificate via a plethora of ways.

## Requirements

N/A

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
TBA
```

## Dependencies

None.

## Example Playbook

```yaml
# The user to create (if they dont exist yet) to run 'acme.sh' as
acme_user: acme

# The group to create (if they dont exist yet) to take ownership of 'acme.sh' certs
acme_group: acme

# Any valid email address
acme_email: test@example.com

# Possible values: "letsencrypt", "zerossl"
# Define the CA to use for certificate creation
acme_ca_server: letsencrypt

# Possible values: "default", "apache"
# Define whether or not to use Apache or to issue the certificates
acme_install:
  mode: default
  config_path: /etc/apache2/sites-enabled/vhosts.conf

# The DNS server configuration - should be fully reusable no matter the service
# See: https://github.com/acmesh-official/acme.sh/wiki/dnsapi
acme_dns:
  provider: dns_autodns
  env:
#     AUTODNS_USER: "test@example.com"
#     AUTODNS_PASSWORD: "password"
#     AUTODNS_CONTEXT: "4"

# Application configuration
# Choose a single main domain and however many SAN domain names as wantd
# Staging will configure 'acme.sh' to ask ACME for staging certificates
# Challenge can either be 'dns','webroot' or 'apache' and controls how certificates are acquired
acme_apps:
  - domain: example.com
    challenge: dns
    webroot: /var/www/example.com
    san: [ ]
    #       - domain: www.example.com
    #         challenge: dns
    #         webroot: /var/www/www.example.com
    #       - domain: test.example.com
    #         challenge: dns
    #         webroot: /var/www/test.example.com
    staging: false
    reloadcmd: sudo systemctl reload apache2
    tls:
      base_path: /etc/tls/certs
      cert_file: /etc/tls/certs/cert.pem
      key_file: /etc/tls/certs/key.pem
      fullchain_file: /etc/tls/certs/fullchain.pem
```

## License

Proprietary

## Author Information

This role was created in 2023 by [Maximilian Gindorfer](https://fmj.dev).
