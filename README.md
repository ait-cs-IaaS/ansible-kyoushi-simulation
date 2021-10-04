# kyoushi simulation

This role installal cr-kyoushi-simulation and cr-kyoushi-statemachines pip modules on the host in order to allow user simulations.

## Requirements

- The server must be installed and configured before executing this role.
- Furthermore, the tasks of this role require the ansible priviledge escalation.

## Role Defaults

| Variable name                                       | Default                                                       | Description                                |
| --------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------ |
| kyoushi_sm_name                                     | *(N/A)*                                                       | Name of the statemachine                   |
| kyoushi_cli                                         | *kyoushi-cli*                                                 | The cli tool name                          |
| kyoushi_sm_effective_name                           | *kyoushi_sm_name* or *kyoushi_sm_python_plugin_name* (if set) | effective sm-name for the rest of the role |
| kyoushi_user_name                                   | *Not set*                                                     | User for file ownership and permissions    |
| kyoushi_user_group                                  | kyoushi_user_name                                             | Group for file ownership and permissions   |
| kyoushi_sim/sm_package_url                          | ait git projects                                              | URL used to install pip package from       |
| **kyoushi_base_packages**                           |                                                               |                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .name                     | ait git projects                                              | pip package name                           |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .url                      | ait git projects                                              | repos url                                  |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .version                  | *(N/A)*                                                       | *optional                                  |
| **kyoushi_additional_packages**                     |                                                               |                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .name                     | *(N/A)*                                                       | pip package name                           |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .version                  | *(N/A)*                                                       | *optional                                  |
| kyoushi_venv_path                                   | /opt/kyoushi/simulation/*sm-name*                             | path to venv                               |
| kyoushi_venv_python_version                         | 3.8                                                           | Python version for venv                    |
| kyoushi_base_path                                   | /etc/kyoushi                                                  |                                            |
| kyoushi_sim_config_path                             | /etc/kyoushi/simulation/*sm-name*                             | path to store the config files             |
| **kyoushi_config_files**                            |                                                               |                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .config                   |                                                               |                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;∟ .src    | config.yml.j2                                                 | local path to config file                  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;∟ .dst    | kyoushi_sim_config_path                                       | remote path to store the config file       |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .sm                       |                                                               |                                            |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;∟ .src    | sm.yml.j2                                                     | local path to sm config file               |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;∟ .dst    | kyoushi_sim_config_path                                       | remote path to store the sm config file    |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;∟ .deploy | *true* if config is defined                                   | controls wheither sm file is deployed      |

## Role optional Defaults

In the following a list of options is given, that are, by default, not set:

## kyoushi sim config

| Variable name                      | Default                             |
| ---------------------------------- | ----------------------------------- |
| kyoushi_plugin_include_names       | ['.*']                              |
| kyoushi_plugin_exclude_names       | []                                  |
| kyoushi_log_level                  | 'WARNING'                           |
| **kyoushi_log_timestamp**          |                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .format  | *(N/A)*                             |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .utc     | 'True'                              |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .key     | 'timestamp'                         |
| **kyoushi_log_console**            |                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .enabled | 'yes'                               |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .format  | 'colored'                           |
| **kyoushi_log_file**               |                                     |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .enabled | 'yes'                               |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .format  | 'json'                              |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .path    | '/var/log/kyoushi/*sm-name*/sm.log' |
| kyoushi_seed                       | *(N/A)*                             |

## kyoushi state machine config

Different depending on the state machine deployed.

## State machine plugin (optional)

| Variable name                  | Default                                                       |
| ------------------------------ | ------------------------------------------------------------- |
| kyoushi_sm_python_plugin_name  | *(N/A)* This overrules kyoushi_sm_name if set                 |
| **kyoushi_sm_python_plugin**   |                                                               |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .src | *kyoushi_sm_python_plugin_name*.py (located in roles *files*) |
| &nbsp;&nbsp;&nbsp;&nbsp;∟ .dst | *kyoushi_sim_config_path*                                     |

## License

GPL-3.0

## Author Information

This role was created in 2021 by Lenhard Reuter
