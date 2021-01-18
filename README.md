Virtual Machine with Windows 95
===============================

Here's a fully configured Windows 95 machine with a working internet
connection, the latest supported version of Netscape Communicator and
Doom 95!

The file `hda.img` contains the harddrive. You can mount it directly
with the `./mount` command to copy over files. The `./start` command
starts the machine using [QEMU](https://www.qemu.org/).


Browsing the internet
---------------------

Windows 95 has been configured to connect to the gateway
`192.168.178.1`. Change this configuration via the `Start -> Settings
-> Control Panel -> Network -> TCP/IP -> Properties -> DNS
Configuration` and `Gateway` tabs.

Netscape Communicator 4.8 has been configured to use the HTTP proxy
server at address `192.168.178.129` port `81`. On this machine I'm
running [nginx](https://nginx.org) with the following configuration:

    server {
      listen 81;

      location / {
        resolver 8.8.8.8;
        proxy_pass https://$host$request_uri;
      }
    }

This allows visiting HTTPS websites over HTTP. To change the proxy
configuration, go to `Edit -> Preferences -> Advanced -> Proxies ->
Manual Proxy Configuration`.


Playing Doom 95
---------------

Microsoft's official Doom port has been installed and there is an icon
on the desktop to launch it. However, the game locks up as soon as you
try to walk. If anyone knows how to solve this, please let me know!


Persisting changes
------------------

First, shutdown Windows 95. Then, type `Ctrl-Alt-2` to switch to the
QEMU monitor, then type `commit all`.
