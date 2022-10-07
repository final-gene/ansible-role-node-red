# Ansible Role `node_red`

## Description

This role allows installing and basically configuring [Node-RED](https://nodered.org/).

It provides a script `/usr/local/bin/node-red-backup` to back up and restore the configuration and flows/projects.

## Requirements

none

## Role Variables

| Variable                                       | Type     | Default                              | Comments                                                                                                                                                                                                                                                   |
|------------------------------------------------|----------|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| nodered_domain_name                            | string   | `{{ inventory_hostname }}`           | Domain name of the Node-Red host.                                                                                                                                                                                                                          |
| nodered_extra_npm_packages                     | array    |                                      | List of NPM packages used by Node-Red.                                                                                                                                                                                                                     |
| nodered_user                                   | string   | `nodered`                            | Name of the user running Node-Red.                                                                                                                                                                                                                         |
| nodered_group                                  | string   | `{{ nodered_user }}`                 | Name of the primary group of the user running Node-Red.                                                                                                                                                                                                    |
| nodered_groups                                 | array    |                                      | List of additional groups the user should belong to.                                                                                                                                                                                                       |
| nodered_allow_low_ports                        | boolean  | `false`                              | Add capability to bind to ports below 1024.                                                                                                                                                                                                                |
| nodered_update_nodes                           | boolean  | `false`                              | Run npm update on existing installed nodes (within scope of package.json).                                                                                                                                                                                 |
| nodered_flow_file                              | string   | `flows.json`                         | Name of the file containing the flow..                                                                                                                                                                                                                     |
| nodered_credential_secret                      | string   |                                      | Key to encrypt stored credentials.                                                                                                                                                                                                                         |
| nodered_config_directory                       | string   |                                      | Directory containing the Node-Red configuration.                                                                                                                                                                                                           |
| nodered_admin_users                            | array    |                                      | [Editor & Admin API security](https://nodered.org/docs/user-guide/runtime/securing-node-red#editor--admin-api-security).                                                                                                                                   |
| nodered_https_private_key_file                 | string   |                                      | Content of the private key file for HTTPS.                                                                                                                                                                                                                 |
| nodered_https_certificate_file                 | string   |                                      | Content of the certificate file for HTTPS.                                                                                                                                                                                                                 |
| nodered_require_https                          | boolean  | `false`                              | Enable HTTPS.                                                                                                                                                                                                                                              |
| nodered_ui_host                                | string   |                                      | Listen address of the UI server.                                                                                                                                                                                                                           |
| nodered_ui_port                                | integer  | `1880`                               | Port the UI server ist listen to.                                                                                                                                                                                                                          |
| nodered_api_max_length                         | string   | `5mb`                                | The maximum size of HTTP request that will be accepted by the runtime api.                                                                                                                                                                                 |
| nodered_lang                                   | string   | `en-US`                              | The preferred language for Node-Red.<br>Available languages: en-US, ja, de, zh-CN, zh-TW, ru, ko                                                                                                                                                           |
| nodered_diagnostics_enabled                    | boolean  | `true`                               | If `true` the Node-Red diagnostics endpoint is enabled.                                                                                                                                                                                                    |
| nodered_diagnostics_ui                         | boolean  | `true`                               | If `true` the Node-Red diagnostics UI is enabled.                                                                                                                                                                                                          |
| nodered_runtime_state_enabled                  | boolean  | `true`                               | If `true` the Node-Red runtime state endpoint is enabled.                                                                                                                                                                                                  |
| nodered_runtime_state_ui                       | boolean  | `true`                               | If `true` the Node-Red runtime state UI is enabled.                                                                                                                                                                                                        |
| nodered_logging_console_level                  | string   | `info`                               | Level of logging to be recorded (see [Logging level](https://nodered.org/docs/user-guide/runtime/logging#level)).                                                                                                                                          |
| nodered_logging_console_metrics                | boolean  | `false`                              | When set to true, the Node-RED runtime outputs flow execution and memory usage information (see [Logging metrics](https://nodered.org/docs/user-guide/runtime/logging#metrics)).                                                                           |
| nodered_logging_console_audit                  | boolean  | `false`                              | When set to true, the Admin HTTP API access events are logged. The event includes additional information such as the end point being accessed, IP address and time stamp (see [Logging audit](https://nodered.org/docs/user-guide/runtime/logging#audit)). |
| nodered_context_storage                        | object   | `default.module: 'memory'`           | Configuration for the context store (see [Context Store API](https://nodered.org/docs/api/context/)).                                                                                                                                                      |
| nodered_external_modules_auto_install          | boolean  | `true`                               | Whether the runtime will attempt to automatically install missing modules.                                                                                                                                                                                 |
| nodered_external_modules_palette_allow_install | boolean  | `true`                               | Enable the Palette Manager in the editor.                                                                                                                                                                                                                  |
| nodered_external_modules_palette_allow_update  | boolean  | `true`                               | Allow modules to be updated in the Palette Manager.                                                                                                                                                                                                        |
| nodered_external_modules_palette_allow_upload  | boolean  | `true`                               | Allow module tgz files to be uploaded and installed.                                                                                                                                                                                                       |
| nodered_external_modules_module_allow_install  | boolean  | `true`                               | Allow node-specified modules to be installed.                                                                                                                                                                                                              |
| nodered_disable_editor                         | boolean  | `false`                              | Disable the editor. The admin API is not affected by this option.                                                                                                                                                                                          |

## Dependencies

- git
- npm >=5.8
- nodejs >=10

## Example Playbook

```yaml

    - name: install Node-Red
      hosts: all
      become: true
      roles:
      - finalgene.node_red
```

## License

MIT

## Author Information

- [Frank Giesecke](https://github.com/frankgiesecke)
