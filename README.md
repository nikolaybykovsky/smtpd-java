# smtpd ![](https://travis-ci.org/jcomo/smtpd.svg?branch=master)

A server implementing the SMTP protocol.

The server is useful for debugging at the moment.
In its current state, the server is only useful for development and debugging.
There is support for sending messages to stdout and to individual files on disk.
Auth and TLS support have not been implemented yet.

### Usage

Download the [pre-release jar](https://github.com/jcomo/smtpd/releases/download/0.1/smtpd.jar).

```
java -jar smtpd.jar
```

To test it, you can point your mail client (such as Apple mail) to the address it is running on, or you can interact with it via telnet.
A example SMTP interaction [from RFC 821](http://www.freesoft.org/CIE/RFC/821/31.htm) can be used.

### Configuration

A properties file can be specified as the first positional argument to the program. Available configuration values are

| Key                       | Default                     | Description                                                                   |
| ------------------------- | --------------------------- | ----------------------------------------------------------------------------- |
| `server.port`             | 8025                        | port to run the server on                                                     |
| `server.hostname`         | contents of `/etc/hostname` | hostname of the mail server                                                   |
| `server.shutdown.timeout` | 5                           | time in seconds to wait for threads to finish before shutting down forcefully |
| `pool.connections.core`   | 0                           | number of unused threads to keep in the server thread pool                    |
| `pool.connections.max`    | 1024                        | max number of simultaneous connections to handle                              |
| `pool.idle.timeout`       | 60                          | time in seconds until idle threads are destroyed                              |
| `mailer.type`             | `debug`                     | the type of Mailer to use for sending mail                                    |
| `mailer.file.directory`   | `/tmp/mail`                 | the directory to use for mail when using the file Mailer                      |

To override this configuration with runtime values, you can use command line properties. All configuration values can be overridden
by suppling the properties with the `smtpd.` prefix. For example, to override the port at runtime:

```
java -Dsmtpd.server.port=5025 -jar smtpd.jar
```
