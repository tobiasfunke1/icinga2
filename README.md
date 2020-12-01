# icinga2

### change ssh port for hosts:
```
hosts.conf
object Host "hostname123" {
...
vars.ssh_port = 1023
...
}

services.conf
apply Service "ssh" {
 ...
 check_command = "ssh"
 vars.port = host.vars.ssh_port
 ...
}

[https://monitoring-portal.org/woltlab/index.php?thread/32752-ssh-monitoring-different-port/]
```
