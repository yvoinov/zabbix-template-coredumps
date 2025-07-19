# Coredumps monitoring template for Zabbix
[![License](https://img.shields.io/badge/License-MIT--Clause-blue.svg)](https://github.com/yvoinov/zabbix-template-coredumps/blob/main/LICENSE)
## Motivation

This template is designed to get a list of cordump names directly in Zabbix notifications, as well as to detect the appearance of new dumps after an alert is triggered.

Unfortunately, due to the limitations of the current LTS version of Zabbix, this functionality could only be implemented using a dual trigger.

Despite the fact that the template was originally developed for Solaris, it can be easily adapted to other operating systems.

Note: Although the templates were developed for Zabbix 7.0, they will work on earlier versions as well. Just adjust the version in the template.

## Using template

Just put Coredumps_development.conf to zabbix_agent.d (zabbix_agent2.d) or add file contents to zabbix_agent.conf (for older agents) and restart agent.

Then import template into Zabbix and apply to host(s).

### How it works

The first trigger detects the appearance of cordumps with a single notification and displays the name/names as a list with a | separator, which allows you to parse the list if necessary, and also display it in notifications quite conveniently (more convenient formatting is impossible due to the limitations of Zabbix and messengers when processing notification text).

The second trigger is designed to track the appearance of multiple subsequent cordumps and update their list in notifications.

The trigger logic is built in such a way as not to spam notifications every minute, the second trigger is triggered only when new dumps appear and is reset after a minute.
