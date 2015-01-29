This is an [Ansible](http://www.ansible.com/home) role for installing
tools for [Riemann](http://riemann.io).

You may also be interested in:

* an Ansible role for
  [Riemann dash](https://github.com/dhruvbansal/riemann-dash-ansible-role),
  a web application used to view data in Riemann
* an Ansible role for
  [Riemann server](https://github.com/dhruvbansal/riemann-server-ansible-role),
  the Rieman server itself

# What it Does

## Software

Installs the Ruby `riemann-client` and `riemann-tools` gems which
provide both the Ruby Riemann client as well as several programs for
basic monitoring of a selected set of services and metrics.

Provides variables which control which of the tools are set up as
system services to feed data to Riemann.  Also creates "configuration
files" for the tools to use to connect to a shared Riemann.  See the
Variables section below.

## Configuration & Logging

Creates the files:

* `/etc/riemann/server_host` -- Riemann server host
* `/etc/riemann/server_port` -- Riemann server port

## Services

FIXME: This was only implemented for Debian...

For each tool used, a system service will be set up running that tool.
For example, the `riemann-health` tool will run as the
`riemann-health` service if the `riemann_tool_health` variable is
true.  See Usage and Variables below.

# Usage

Use the role in a playbook like this:

```yaml
- hosts: all
  roles:
    - role: riemann-client
	  riemann_tool_health: true
      ...
```

The `riemann-client` role will install the Riemann tools and the Ruby
Riemann client.  Setting `riemann_tool_health` will cause the
`riemann-health` tool to be run as the `riemann-health` service.  See
Variables below.

# Variable

The following variables are used for configuring which tools are
launched as services and how:

## Global Settings:
* `riemann_server_host` -- the host for the Riemann server (default: 127.0.0.1)
* `riemann_server_port` -- the port for the Riemann server (default: 5555)

## Specific Tools

### riemann-health

* `riemann_tool_health` -- launches the `riemann-health` service

### riemann-elasticsearch

* `riemann_tool_elasticsearch` -- launches the `riemann-elasticsearch` service
* `elasticsearch_host` -- the ElasticSearch host to monitor

### riemann-nginx-status

* `riemann_tool_nginx` -- launches the `riemann-nginx` service
* `nginx_status_uri` -- the URI at which nginx reports metrics
