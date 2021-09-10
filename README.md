# MinIO

| master |
| -------- |
| [![Build Status](https://drone.osshelp.ru/api/badges/ansible/minio/status.svg)](https://drone.osshelp.ru/ansible/minio) |

Role for MinIO server and MinIO client installation.

## Deploy example (only server with default params, barely usable)

```yaml
  roles:
    - minio
```

## Example with custom parameters(do not copy blindly)

```yaml
    - { role: minio,
        minio_install_client: true,
        minio_place_policies: true,
        minio_server: {
          bind_address: 0.0.0.0,
          bind_port: 9000,
          cluster_members: [],
          volume: "/var/lib/minio/data",
          access_key: access_key_from_vault,
          secret_key: secret_key_from_vault,
          browser: "off",
          region: "local",
          domain: "somedomain.tld",
          options: "--anonymous"
        }
    }
```

## Available parameters

### Main

| Param | Default | Description |
| -------- | -------- | -------- |
| `minio_setup` | `full` | Setup mode. See [OSSHelp KB article](https://oss.help/kb4895) |
| `minio_server_version` | see [defaults](defaults/main.yml) | MinIO server version to install. |
| `minio_client_version` | same as `minio_server_version` | MinIO client version to install. |
| minio_install_server | `true` | Whether to install/configure MinIO server. |
| minio_install_client | `false` | Whether to install/configure MinIO client. |
| minio_place_policies | `false` | Whether or not to initiate the policy placing mechanism. |
| minio_policies.source | `files/minio/polices` | Relative path to directory with polices in repo. |
| minio_policies.target | `/etc/minio/policies` | Relative path to directory on target, where policies must be placed. |

### MinIO server params

Should be set as a dictionary `minio_server` (see example above).

| Param | Default | Description |
| -------- | -------- | -------- |
| bind_address | `0.0.0.0` |  |
| bind_port | `9000` | |
| cluster_members | - | |
| volume | `/var/lib/minio/data` | |
| access_key | - | Access key, that will be used for admin access. |
| secret_key | - | Secret key, that will be used for admin access. |
| browser | `off` | Wheter or not browser UI should be available. |
| region | `local` | Name of the location of the server e.g. "us-west-rack2" |
| domain | - | Used to enable virtual-host-style requests. If the request `Host` header matches with `(.+).mydomain.com` then the matched pattern $1 is used as bucket and the path is used as object. |

### MinIO client params

Should be set as a dictionary `minio_client`. No need to change theese without necessity.

| Param | Default | Description |
| -------- | -------- | -------- |
| download_url | `https://oss.help/builds/minio/mc` | URL to download MinIO client binary from. |
| binary_dir | `/usr/local/bin` | Directory where the binary will be placed. |
| config | `/root/.minio-client/config.json` | Absolute path to client configuration file. |
| default_host | `local` | S3 host, thet will be used by default. |

### Misc

No need to change theese without strong necessity.

| Param | Default | Description |
| -------- | -------- | -------- |
| minio_user | `minio` | User, which will be used to run MinIO server. |
| minio_download_url | `https://oss.help/builds/minio/minio` | URL to download MinIO server binary from. |
| minio_download_checksums | `https://oss.help/builds/minio/SHA256SUMS` | URL to MinIO server binary checksums file. |
| minio_conf_dir | `/etc/minio` | Absolute path to MinIO server configuration directory. |
| minio_working_dir | `/usr/local` | Absolute path to MinIO server working directory. |
| minio_binary_dir | `/usr/local/sbin` | Absolute path to MinIO server binary directory. |
| minio_templates_dir | `/usr/local/osshelp` | Absolute path to directory with templates (e.g. policies). |
| minio_log_dir | `/var/log/minio` | Absolute path to MinIO server log directory. |

## FAQ

None, so far.

## Useful links

- [Official documentation](https://docs.min.io/docs/minio-quickstart-guide.html)
- [Our article](https://oss.help/kb3703)

## TODO

- Check the role in various builds
- Improve tests
- Improve readme
- Focal support for new MinIO versions

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
