# Init

* Automatically adopts all orphaned processes
* Typically assigned PID=1
* SystemVInit, launchd, daemontools, runit, Upstart, systemd

## runit

* [runit-quickstart](https://kchard.github.io/runit-quickstart/)

`runsvdir` watch the `/etc/service` directory and start a new `runsv` process to manage the service.

* Reimplementation of daemontools
* Parallelization of the start up of system services which speed up boot time
* Used by Void Linux
* Can be used to replace sysvinit, or just use as a service supervisor
* Does not require pidfile??
* Reliable logging??
* Once you stop a service with `sv stop <SERVICE>`, it will not be restarted automatically


Focus on 3 things:

1. One time initialization
2. Process supervision - ability to restart services which have failed
3. Halting or rebooting

## Upstart

## systemd



