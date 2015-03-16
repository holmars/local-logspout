# Local logspout test setup

We start logspout without any routes, since we don't want to get stdout/stdout from all containers.

To create a route run the following:
```
curl http://docker:81/routes -X POST \
    -d '{"source": {"filter": "devpi-master"}, "target": {"type": "syslog", "addr": "logstashshipper:5000"}}'
```
This will route both stdout and stderr from devpi-master to our logstashshippper, which will output the logs to redis.

To list all routes:
```
curl http://docker:81/routes
```

See [logspout's docs](https://github.com/gliderlabs/logspout) for more information.

## Logstash-shipper

Currently we need to include this logstash-shipper to handle the syslog to redis part of the (R)ELK pipeline. Hopefully https://github.com/gliderlabs/logspout/pull/41 will get merged soon.
