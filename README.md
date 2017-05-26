# Drone.io

[Drone](http://readme.drone.io/) is a Continuous Integration platform built on container technology. Every build is executed inside an ephemeral Docker container, giving developers complete control over their build environment with guaranteed isolation.


This chart installs Drone `0.7.1` using an Ingress Rule and a Postgres database (this chart doesn't install the database).

Before installing Drone you need to setup your Ingres Controller, DNS, Github OAuth Application and the Database. Once you have all those things properly configured, you can execute the following command and it will install drone in your kubernetes cluster.

```bash

$ export GITHUB_CLIENT=xxx
$ export GITHUB_SECRET=xxx
$ export DATASOURCE=postgres://droneadmin:P1P4BTqd2XLw@data-postgres:5432/drone?sslmode=disable
$ export TLS_CERT=xxx
$ export TLS_KEY=xxx
$ export HOST=drone.example.com

$ helm upgrade --install build . --debug --set github.secret=$GITHUB_SECRET,github.client=$GITHUB_CLIENT,shared_secret=$SECRET,database.datasource=$DATASOURCE,tls.crt=$TLS_CERT,tls.key=$TLS_KEY,ingress.host=$HOST
```

To access it, you will need to go to `https://$HOST`, the Ingress Rule has an automatic http-https redirection. Note as well that you need to specify the TLS data. You can disable TLS by adding `ingess.ssl=false` to the Helm command.