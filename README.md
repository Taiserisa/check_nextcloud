# check_nextcloud

This is a monitoring plugin for [icinga](https://www.icinga.com) to check the status of the [nextcloud](https://nextcloud.com) serverinfo API.

![Icingaweb2 screenshot showing the check_nextcloud script](/screenshot.png?raw=true "Icingaweb2 screenshot")


## Usage
Try the plugin at the command line like this:
```
/usr/bin/php ./check_nextcloud.php -H cloud.example.com -T access-token

```

You can define the icinga2 check command as follows:
```
object CheckCommand "nextcloud" {
  import "plugin-check-command"

  command = [ PluginDir + "/check_nextcloud.php" ]

  arguments = {
    "-H" = {
      "required" = true
      "description" = "Nextcloud hostname/fqdn (e.g. 'cloud.example.com')"
      "value" = "$nc_host$"
    }
    "-U" = {
      "required" = false
      "description" = "serverinfo API url, you can find it on https://cloud.example.com/settings/admi$
      "value" = "$nc_api_url$"
    }
    "-T" = {
      "required" = false
      "description" = "server info token - define it here https://cloud.example.com/index.php/settings/admin/serverinfo"
      "value" = "$nc_api_user$"
    }
    "-u" = {
      "required" = false
      "description" = "API user (has to be an admin) - obsolete when -T provided"
      "value" = "$nc_api_user$"
    }
    "-p" = {
      "required" = false
      "description" = "API-user's password - obsolete when -T provided"
      "value" = "$nc_api_password$"
    }

  }

  vars.nc_api_url = "/ocs/v2.php/apps/serverinfo/api/v1/info"
}
```

## Changelog
* 2019-05-08: initial version (koelle25)
* 2023-04-07: add token athentification (beccon4)
## Authors
* [Kevin Köllmann](https://github.com/koelle25)
* [Conrad Beckert](https://github.com/beccon4)
