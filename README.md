newrelic_plugin_agent
=====================

Agent that polls supported backend systems and submits the results to the
NewRelic platform. Currently supported backend systems are:

- CouchDB
- Memcached
- RabbitMQ
- Redis

Installation Instructions
-------------------------



Configuration Example
---------------------

    %YAML 1.2
    ---
    Application:
      license_key: VALUE
      poll_interval: 60

      couchdb:
        name: localhost
        host: localhost
        port: 5984

      memcached:
        name: localhost
        host: localhost
        port: 11211

      rabbitmq:
        name: rabbitmq@localhost
        host: localhost
        port: 15672
        username: guest
        password: guest

      redis:
        - name: localhost
          host: localhost
          port: 6379
          db_count: 16

    Daemon:
      pidfile: /var/run/newrelic_plugin_agent.pid

    Logging:
      formatters:
        verbose:
          format: '%(levelname) -10s %(asctime)s %(process)-6d %(processName) -15s %(threadName)-10s %(name) -25s %(funcName) -25s L%(lineno)-6d: %(message)s'
      handlers:
        file:
          class : logging.handlers.RotatingFileHandler
          formatter: verbose
          filename: /tmp/newrelic_plugin_agent.log
          maxBytes: 10485760
          backupCount: 3
      loggers:
        newrelic_plugin_agent:
          level: INFO
          propagate: True
          handlers: [console, file]
        requests:
          level: ERROR
          propagate: True
          handlers: [console, file]
