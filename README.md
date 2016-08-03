# Consul Configuration

 Consul uses client agents and RAFT to provide a consistent view of services.
 Consul can monitor and change services topology based on health of individual nodes.

### Setting up a local consul cluster

A consul agent runs in server mode or client mode. Server agents maintain the state of the cluster. You want to have three to 5 server agents per datacenter. Client agents are used on the servers whose services you want to monitor and report back to the consul servers. We will install three server and three client mode. You have to install all consul client on your infrastructure.

## Server 1. Configuration

```
{
  "datacenter": "localdatacenter",
  "data_dir": "/Desktop/consul1",
  "log_level": "INFO",
  "node_name": "localserver1",
  "skip_leave_on_interrupt": true,
  "leave_on_terminate": true,
  "server": true,
  "bootstrap" : true,
  "acl_datacenter": "localdatacenter",
  "acl_master_token": "123456",
  "acl_default_policy": "deny",
  "ports" : {
    "dns" : -1,
    "http" : 9500,
    "rpc" : 9400,
    "serf_lan" : 9301,
    "serf_wan" : 9302,
    "server" : 9300
  }
}
```

When you are starting up a new server cluster you typically put one of the servers inbootstrap mode. This tells consul that this server is allowed to elect itself as leader. It is like when you ask Dick Chenney to be on the VP selection committee and he nominates himself

## Server 2. Configuration

```
{
  "datacenter": "localdatacenter",
  "data_dir": "/Desktop/consul2",
  "log_level": "INFO",
  "node_name": "localserver2",
  "skip_leave_on_interrupt": true,
  "leave_on_terminate": true,
  "server": true,
  "bootstrap" : false,
  "acl_datacenter": "localdatacenter",
  "acl_master_token": "123456",
  "acl_default_policy": "deny",
  "ports" : {
    "dns" : -1,
    "http" : 9500,
    "rpc" : 9400,
    "serf_lan" : 9301,
    "serf_wan" : 9302,
    "server" : 9300
  }
}
```

## Server 3. Configuration
```
{
  "datacenter": "localdatacenter",
  "data_dir": "/Desktop/consul3",
  "log_level": "INFO",
  "node_name": "localserver3",
  "skip_leave_on_interrupt": true,
  "leave_on_terminate": true,
  "server": true,
  "bootstrap" : false,
  "acl_datacenter": "localdatacenter",
  "acl_master_token": "123456",
  "acl_default_policy": "deny",
  "ports" : {
    "dns" : -1,
    "http" : 9500,
    "rpc" : 9400,
    "serf_lan" : 9301,
    "serf_wan" : 9302,
    "server" : 9300
  }
}
```

## Client 1. Configuration

```
{
  "datacenter": "localdatacenter",
  "data_dir": "/Desktop/web",
  "ui_dir":"/Desktop/web",
  "log_level": "INFO",
  "server": false,
  "node_name": "client1",
  "skip_leave_on_interrupt": true,
  "leave_on_terminate": true,
  "acl_datacenter": "localdatacenter",
  "acl_master_token": "123456",
  "acl_default_policy": "deny",
  "ports" : {

    "dns" : -1,
    "http" : 8500,
    "rpc" : 8400,
    "serf_lan" : 8301,
    "serf_wan" : 8302,
    "server" : 8300
  },


  "start_join" : [
    "127.0.0.1:9301",
    "127.0.0.1:10301",
    "127.0.0.1:11301"
    ]
}
```
