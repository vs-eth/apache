# Apache

Role for setting up Apache2, optionally including Switch AAI.

## Configuration
| Variable name | Default value | Description |
|---------------|---------------|-------------|
| `apache_modules` | `{"name": "ssl", "state": "present"}` | List of modules to activate/deactivate |
| `apache_sites` | `[{"name": "vhosts.conf", "state": "link"}, {"name": "000-default", "state": "absent"}]` | Lists of sites to either disable (absent) or enable (link) |
| `apache_create_vhosts` | `true` | Whether this role is supposed to create a vhost |
| `apache_vhosts_filename` | `vhosts.conf` | Name of the vhost to create |
| `apache_listen_ip` | `*` | Listen on this address |
| `apache_listen_port` | `80` | Port to listen on for HTTP |
| `apache_listen_port_ssl` | `443` | Port to listen on for HTTPS |
| `apache_global_vhost_settings` | `DirectoryIndex index.php index.html` | Settings to apply to all vhosts |
| `apache_vhosts` | (see defaults/main.yml) | Vhost configuration for HTTP vhosts |
| `apache_vhosts_ssl` | `[]` | Vhost configuration for HTTPs vhosts |
| `apache_ignore_missing_ssl_certificate` | `true` | Whether to ignore missing SSL certificates |
| `apache_ssl_protocol` | `All -SSLv2 -SSLv3` | TLS/SSL versions to enable |
| `apache_ssl_cipher_suite` | (see defaults/main.yml) | Ciphers to enable. For more information, see [Mozilla's excellent wiki](https://wiki.mozilla.org/Security/Server_Side_TLS) |
| `apache_sslonly` | `False` | Whether to restrict apache to only serve a HTTPS redirect via HTTP |
| `apache_aai` | False | Whether to enable support for Switch AAI (see below) |
| `apache_aai_config_loc` | `{{ config_repo_path }}/shib/{{ ansible_fqdn }}` | Where to find the config files for AAI |

For example vhosts, have a look at `defaults/main.yml`.

### Switch AAI
This role supports configuring Apache to act as a Shibboleth service provider, which is
intended to be used with [Switch AAI](https://www.switch.ch/aai/). When the support is enabled, this role adds the Switch AAI repo, installs shibboleth and uploads the necessary configuration, which can be obtained by completing the [Switch AAI Shibboleth SP Configuration Guide](https://www.switch.ch/aai/guides/sp/configuration/). If no shibboleth certficate (different from the Apache certificate) is found, a new one with a validity of 3 years will be generated.

## License
GPLv3
