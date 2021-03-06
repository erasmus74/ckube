# Concurrent kubectl
![Kelsey Hightower Approved!](https://img.shields.io/badge/Hightower-approved-blue.svg) [![Build Status](https://travis-ci.org/devonmoss/ckube.svg?branch=master)](https://travis-ci.org/devonmoss/ckube) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A cli to simplify working with kubectl for some common workflows

#### Installation
Find the latest binaries [here](https://github.com/devonmoss/ckube/releases/)

#### Usage
`ckube` lets you think in terms of [services](https://kubernetes.io/docs/concepts/services-networking/service/) instead of [pods](https://kubernetes.io/docs/concepts/workloads/pods/pod/) (mostly).


```$xslt
$ ckube
A CLI to simplify working with kubectl.

Usage:
  ckube [command]

Available Commands:
  exec        execute a command in a container
  help        Help about any command
  logs        get logs from a service
  ls          list pods in kubernetes
  nodes       Lists pods grouped by node
  top         View cpu and memory usage for pods

Flags:
      --context string      the kubernetes context (defaults to value currently used by kubectl)
  -h, --help                help for ckube
      --kubeconfig string   path to kubeconfig file to use for CLI requests (defaults to $HOME/.kube/config)
  -l, --labels string       Selector (label query) to filter on, supports '=', '==', and '!='.(e.g. -l key1=value1,key2=value2)
  -n, --namespace string    the kubernetes namespace (defaults to value currently used by kubectl)

Use "ckube [command] --help" for more information about a command.


```

Kubernetes services are often an abstraction over multiple pods, particularly if the replicas are scaled. If a k8s cluster has a service called `nginx` you could have several pods which might be named something like this:
```$xslt
nginx-3528986049-kpd4z
nginx-3528986049-71s10 
nginx-3528986049-f6mwf
nginx-3528986049-ltx6j
nginx-3528986049-m3cmm
nginx-3528986049-h8cnn
nginx-3528986049-6v4c1
```

Getting logs for the nginx service is easy with `ckube`
```
# single uspecified nginx pod:
ckube logs nginx

# all nginx pods
ckube logs nginx -a

# follow the logs
ckube logs nginx -f
```
![](https://github.com/devonmoss/ckube/blob/master/images/logs.gif?raw=true)

Similar concurrent functionality exists for `exec`
![](https://github.com/devonmoss/ckube/blob/master/images/exec.gif?raw=true)

![](https://github.com/devonmoss/ckube/blob/master/images/complex-exec.gif?raw=true)

Read the blog post about `ckube` [here](https://devonmoss.com/concurrent-kubectl)

#### Contributing
PR's accepted

If you are looking to build the project:
```$xslt
go get -d github.com/devonmoss/ckube
cd $GOPATH/src/github.com/devonmoss/ckube
```
