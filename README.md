# loopback-connector-readsplitmysql
This is an entirely compatible fork of the mysql connector module that adds read/write splitting.
`loopback-connector-mysql` is the MySQL connector module for [loopback-datasource-juggler](https://github.com/strongloop/loopback-datasource-juggler/).

For complete documentation of the mysql connector, see [StrongLoop Documentation | MySQL Connector](http://loopback.io/doc/en/lb2/MySQL-connector.html).

Read/Write splitting allows loopback to take advantage of Read-Replicas by directing all read-only queries
to faster read replica slaves, whilst writes are sent to the master database.

## Installation

````sh
npm install loopback-connector-readsplitmysql --save
````

## Basic use
The read split connector can be used in-place of the latest 2x mysql connector. With no additional
configuration it will continue to operate against one master database.

To add a read-replica host, add a `readonly` object to the settings object. All fields are optional.
The database connection options will default to the same as the master connection. To disable the read
client, either don't set the `readonly` options at all or set the `writeRatio` to 1.

| Option                | Default    | Description                                                      |
| --------------------- | ---------- | ---------------------------------------------------------------- |
| `readonly.writeRatio` | 0.3        | The fraction of connectionLimit to dedicate to write connections |
| `readonly.host`       | `host`     | The host for read-only queries                                   |
| `readonly.port`       | `port`     | The port for read-only queries                                   |
| `readonly.user`       | `user`     | The user for read-only queries                                   |
| `readonly.password`   | `password` | The password for read-only queries                               |