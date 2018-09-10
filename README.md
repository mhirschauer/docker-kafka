Kafka in Cloudfoundry
===

This repository provides everything you need to run Kafka in Cloudfoundry as a app.

Be aware that this is ONLY for testing a Kafka connection. The Cloudfoundry containers are stateless, 
this means that you will loose every information about consumers and also the messages itself when
it is restarted.

If you know that you will get a Kafka in a seperate hosted enviroment or as a service in Cloudfoundry later
then it can be a start for the development process.

For convenience also contains a packaged proxy that can be used to get data from
a legacy Kafka 7 cluster into a dockerized Kafka 8.

Why?
---
The main hurdle of running Kafka in Cloudfoundry is that there is a default port 8080 that is open
but not others. Therefore the internal port is changed and not only the mapping.
Mappings will not work in Cloudfoundry


The main hurdle of running Kafka in Docker is that it depends on Zookeeper.
Compared to other Kafka docker images, this one runs both Zookeeper and Kafka
in the same container. This means:

* No dependency on an external Zookeeper host, or linking to another container
* Zookeeper and Kafka are configured to work together out of the box

Run in cloudfoundry
-------------------

```bash
cf push <app_name> --docker-image mhirschauer/kafka-cloudfoundry-app
```

Run locally
-----------

```bash
docker run -p 2181:2181 -p 9092:8080 --env ADVERTISED_PORT=8080 --env INTERNAL_PORT=8080 spotify/kafka
```

Public Builds
---

https://registry.hub.docker.com/u/mhirschauer/kafka-cloudfoundry-app/

Build from Source
---

    docker build -t mhirschauer/kafka-cloudfoundry-app kafka/

Todo
---

* Not particularily optimized for startup time.
* Better docs

