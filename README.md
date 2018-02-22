<!--
#                                 __                 __
#    __  ______  ____ ___  ____ _/ /____  ____  ____/ /
#   / / / / __ \/ __ `__ \/ __ `/ __/ _ \/ __ \/ __  /
#  / /_/ / /_/ / / / / / / /_/ / /_/  __/ /_/ / /_/ /
#  \__, /\____/_/ /_/ /_/\__,_/\__/\___/\____/\__,_/
# /____                     matthewdavis.io, holla!
#
#-->

[![Clickity click](https://img.shields.io/badge/k8s%20by%20example%20yo-limit%20time-ff69b4.svg?style=flat-square)](https://k8.matthewdavis.io)
[![Twitter Follow](https://img.shields.io/twitter/follow/yomateod.svg?label=Follow&style=flat-square)](https://twitter.com/yomateod) [![Skype Contact](https://img.shields.io/badge/skype%20id-appsoa-blue.svg?style=flat-square)](skype:appsoa?chat)

# Confluence on Kubernetes backed by PersistentVolumeClaim

> k8 by example -- straight to the point, simple execution.

Like to helm? Check out https://github.com/mateothegreat/helm-chart-atlassian-confluence

## Usage

```sh
$ make help

                                __                 __
   __  ______  ____ ___  ____ _/ /____  ____  ____/ /
  / / / / __ \/ __  __ \/ __  / __/ _ \/ __ \/ __  /
 / /_/ / /_/ / / / / / / /_/ / /_/  __/ /_/ / /_/ /
 \__, /\____/_/ /_/ /_/\__,_/\__/\___/\____/\__,_/
/____
                        yomateo.io, it ain't easy.

Usage: make <target(s)>

Targets:

  initdb               Create mysql database & grant (DROP DATABASE is performed!)
  git/update           Update submodule(s) to HEAD from origin
  install              Installs manifests to kubernetes using kubectl apply (make manifests to see what will be installed)
  delete               Deletes manifests to kubernetes using kubectl delete (make manifests to see what will be installed)
  get                  Retrieves manifests to kubernetes using kubectl get (make manifests to see what will be installed)
  describe             Describes manifests to kubernetes using kubectl describe (make manifests to see what will be installed)
  context              Globally set the current-context (default namespace)
  shell                Grab a shell in a running container
  dump/logs            Find first pod and follow log output
  dump/manifests       Output manifests detected (used with make install, delete, get, describe, etc)
```

## Install

```sh
$ make install

[ DEPLOYING manifests/deployment.yaml ]: deployment "atlassian-confluence" created
[ DEPLOYING manifests/persistentvolumeclaim.yaml ]: persistentvolumeclaim "atlassian-confluence-persistent-storage" created
[ DEPLOYING manifests/service.yaml ]: service "atlassian-confluence" created

```

## Logs

```sh
$ make dump/logs
...
kubectl --namespace default logs -f atlassian-confluence-57f4c59ccf-l8s9x
User is currently root. Will change directory ownership to daemon:daemon, then downgrade permission to daemon
executing as current user
If you encounter issues starting up Confluence, please see the Installation guide at http://confluence.atlassian.com/display/DOC/Confluence+Installation+Guide

Server startup logs are located in /opt/atlassian/confluence/logs/catalina.out
---------------------------------------------------------------------------
Using Java: /usr/lib/jvm/java-1.8-openjdk/bin/java
2018-02-19 07:40:42,896 INFO [main] [atlassian.confluence.bootstrap.SynchronyProxyWatchdog] A Context element for ${confluence.context.path}/synchrony-proxy is found in /opt/atlassian/confluence/conf/server.xml. No further action is required
---------------------------------------------------------------------------
19-Feb-2018 07:40:43.597 WARNING [main] org.apache.tomcat.util.digester.SetPropertiesRule.begin [SetPropertiesRule]{Server} Setting property 'debug' to '0' did not find a matching property.
...
```

## Delete

```sh
$ make delete
```
