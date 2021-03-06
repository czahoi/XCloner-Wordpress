# xcloner-core

## Installation

Local composer.json should contain this custom repository for now

```
"repositories": [
        {
            "type": "vcs",
            "packagist": false,
            "url":  "https://github.com/watchfulli/xcloner-core.git"
        }
    ]
 ```

then 

```composer require watchfulli/xcloner-core```

## Usage

Trigger standalone backup with profile stored in standalone_backup_trigger_config.json

```
<?php
define('WP_DEBUG', true);
define('WP_DEBUG_DISPLAY', true);

require_once('../vendor/autoload.php');

$profile = [
    'id' => 0
];

//loading the default xcloner settings in format [{'option_name':'value', {'option_value': 'value'}}]
$json_config = json_decode(file_get_contents(__DIR__ . '/standalone_backup_trigger_config.json'));

if (!$json_config) {
    die('Could not parse default JSON config, i will shutdown for now...');
}

//pass json config to Xcloner_Standalone lib
$xcloner_backup = new watchfulli\XClonerCore\Xcloner_Standalone($json_config);

$xcloner_backup->start($profile['id']);

```


### standalone_backup_trigger_config.json

```
[
{"option_name":"xcloner_cleanup_retention_limit_archives","option_value":"100"},
{"option_name":"xcloner_cleanup_retention_limit_days","option_value":"60"},
{"option_name":"xcloner_cleanup_settings_page","option_value":""},
{"option_name":"xcloner_cron_settings_page","option_value":""},
{"option_name":"xcloner_database_records_per_request","option_value":"1000"},
{"option_name":"xcloner_db_version","option_value":"1.1.7"},
{"option_name":"xcloner_directories_to_scan_per_request","option_value":"1000"},
{"option_name":"xcloner_disable_email_notification","option_value":"1"},
{"option_name":"xcloner_enable_log","option_value":"1"},
{"option_name":"xcloner_enable_mysql_backup","option_value":"1"},
{"option_name":"xcloner_enable_pre_update_backup","option_value":""},
{"option_name":"xcloner_encryption_key","option_value":"FMo5vh64rNCrTo8zcmTsrzV88nnHj6BGOAK"},
{"option_name":"xcloner_standalone_api_key","option_value":""},
{"option_name":"xcloner_exclude_files_larger_than_mb","option_value":"0"},
{"option_name":"xcloner_files_to_process_per_request","option_value":"328"},
{"option_name":"xcloner_force_tmp_path_site_root","option_value":"1"},
{"option_name":"xcloner_mysql_database","option_value":"wordpress"},
{"option_name":"xcloner_mysql_hostname","option_value":"localhost"},
{"option_name":"xcloner_mysql_password","option_value":"root"},
{"option_name":"xcloner_mysql_prefix","option_value":"wp_"},
{"option_name":"xcloner_mysql_settings_page","option_value":""},
{"option_name":"xcloner_mysql_username","option_value":"root"},
{"option_name":"xcloner_size_limit_per_request","option_value":"50"},
{"option_name":"xcloner_split_backup_limit","option_value":"2048"},
{"option_name":"xcloner_start_path","option_value":"\/Applications\/MAMP\/htdocs\/wordpress/"},
{"option_name":"xcloner_store_path","option_value":"\/Applications\/MAMP\/htdocs\/wordpress\/wp-content\/backups\/"},
{"option_name":"xcloner_system_settings_page","option_value":"100"},
{"option_name":"xcloner_text","option_value":"0"},
{"option_name":"profile", "option_value":{
  "extra": [],
  "backup_params": {
    "backup_name": "backup_[domain]_8888-[time]-sql",
    "email_notification": "info@noreply.com",
    "diff_start_date": "",
    "schedule_name": "test2",
    "backup_encrypt": false,
    "start_at": false,
    "schedule_frequency": "daily",
    "schedule_storage": ""
  },
  "database": {
    "#": [
      "wordpress",
      "joomla"
    ]
  },
  "excluded_files": [
    "wp-content",
    "wp-includes"
  ]
}}
]
```
