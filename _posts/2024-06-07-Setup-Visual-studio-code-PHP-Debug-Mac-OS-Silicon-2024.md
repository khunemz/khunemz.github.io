---
layout: post
title:  "Setup Visual studio code PHP Debug Mac OS Silicon 2024"
author: m_chutipong
categories: [ php ]
image: assets/images/posts/20240706/vscode.png
---
## Prerequisition:

- php 8.3 installed by brew see => https://formulae.brew.sh/formula/php
- the xdebug.so has been already installed see => https://xdebug.org/docs/install#pecl
- You have already installed visual studio code => https://code.visualstudio.com/

1) check you installation path:

```
which php
# it should show
# /opt/homebrew/bin/php
```

2) check xdebug.so has already added in this directory `/opt/homebrew/Cellar/php/8.3.8/pecl/20230831/xdebug.so`
3) Update the **php.ini**, if you do not know the **php.ini** located you can check by this command:
```
php --ini
```
it should show:
```
Configuration File (php.ini) Path: /opt/homebrew/etc/php/8.3
Loaded Configuration File:         /opt/homebrew/etc/php/8.3/php.ini
Scan for additional .ini files in: /opt/homebrew/etc/php/8.3/conf.d
Additional .ini files parsed:      /opt/homebrew/etc/php/8.3/conf.d/ext-opcache.ini
```
4) update the **/opt/homebrew/etc/php/8.3/php.ini** by adding this chunk of code in the end of file:
```
[xdebug]
zend_extension="/opt/homebrew/Cellar/php/8.3.8/pecl/20230831/xdebug.so"
xdebug.mode=debug
xdebug.client_host=localhost
xdebug.client_port=9003
xdebug.discover_client_host=true
xdebug.start_with_request=yes
xdebug.log_level=0
```
Then save and restart php by using this command:
```
brew services restart php
# result should be like this

# Stopping `php`... (might take a while)
# ==> Successfully stopped `php` (label: homebrew.mxcl.php)
# ==> Successfully started `php` (label: homebrew.mxcl.php)
```
5) The visual studio code, you must install the `PHP Debug` extension:

![extension]({{ site.baseurl }}/assets/images/20240706/vscode.png)

   
6) Update `launch.json` file by adding the configuration like this:

```
{
        "name": "Listen for Xdebug",
        "type": "php",
        "request": "launch",
        "port": 9003,
        "pathMappings": {
            "${workspaceFolder}": "${workspaceFolder}"
        },
}
```

7) Try run debugging, go to menu **run > start debugging** and try adding break point somewhere in the code that you app can reach that line:

![extension]({{ site.baseurl }}/assets/images/20240706/debuggin.png)

Enjoy building app with PHP ❤️