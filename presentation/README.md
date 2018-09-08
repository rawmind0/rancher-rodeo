
# Rancher rodeo

This repo contains markdown slides to generate Rancher rodeo 2.x presentation.

## Presentation 

Presentation is done by [reveal.js][reveal.js]. Default config and slides sections are defined at `index.html` file. 

If you add new module, you need to add it at `index.html` file.

More info about config at [reveal configuration][reveal-config]

## Rodeo modules

- Introdutcion
  - What is a container?
  - Is a container like a VM?
  - Why use containers?
  - What is Docker?
  - Docker architecture
  - What is Kubernetes?
  - Kubernetes architecture
  - Kubernetes deployment Types
  - What is Rancher?
  - Rancher 2.x architecture
- Practice
  - Prerequisites
  - Vagrant users
  - Running Rancher 2.x
  - Creating k8s cluster
  - Installing kubectl
  - Deploying Wordpress from Catalog
  - Persistent Storage
    - Setting up the NFS server
    - Setting up the NFS class and provisioner
  - Deploying Wordpress from Catalog using Persistent Storage

## Build

Build to get a docker image with rancher rodeo packaged to be presented.

```
docker build -t rancher/rancher-rodeo:<version> .
```

Image comes from [alpine-revealjs][alpine-revealjs]. To upgrade reveal.js, update `FROM rawmind/alpine-revealjs:3.6.0-0` in the Dockerfile to the desired version and build the docker.

## Run

Once docker image is built, it could be run locally, at Rancher system or added to a rancher training catalog. 
Service will be exposed on port 8080 by default.

```
docker run -td -p 8080:8080 rancher/rancher-rodeo:<version>
```

Rancher rodeo modules could be accessed from your web browser, http://localhost:8080

## Save to pdf

Once Rancher rodeo image is server at http://localhost:8080, to get pdf version:

- Access to http://localhost:8080/?print-pdf or click in rancher image at http://localhost:8080/#/
- Training module is showed in a single page. 
- Go to Print - Save as pdf at web browser with this options

![Save as pdf](https://camo.githubusercontent.com/e3b3088a2dd7a53caf72de529b3ce41465dd99f0/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f68616b696d2d7374617469632f72657665616c2d6a732f7064662d7072696e742d73657474696e67732d322e706e67)

[reveal.js]: https://github.com/hakimel/reveal.js
[reveal-config]: https://github.com/hakimel/reveal.js#configuration
[alpine-revealjs]: https://github.com/rawmind0/rawmind/alpine-revealjs/
