wercker-docker-sample
=====================

[![wercker status](https://app.wercker.com/status/2f457dbea0d4f80c1d675d5b9c153a89/m "wercker status")](https://app.wercker.com/project/bykey/2f457dbea0d4f80c1d675d5b9c153a89)

This is a sample app to demonstrate [docker](http://docker.io) support on [wercker](http://wercker.com).

### What is docker?

Docker is an exciting open-source project to pack, ship and run any application as a lighthweight portable container. 
Developers and system administrators can author lightweight images that provide a pristine state that encapsulates an application.

Think of it as a way to pack your application as a virtual machine, without the overhead and performance penalty of the hypervisor.

If you want to learn more about docker, here is a list of resources we like:

* [Docker: Using Linux Containers to Support Portable Application Deployment (infoq.com)](http://www.infoq.com/articles/docker-containers/)
* [navigate through your infrastructure with docker (jolicode.com)](http://jolicode.com/blog/navigate-through-your-infrastructure-with-docker)
* [PaaS Evolves with Linux Containers and OpenStack (openshift.com)](https://www.openshift.com/blogs/paas-evolves-with-linux-containers-and-openstack)
* and of course the Docker [homepage](http://docker.io)

### Common scenario's

We are exited to see how docker will be used. In the conversations we've had with our users we distilled the following three scenarios:

1. Testing a [Dockerfile](http://docs.docker.io/en/latest/use/builder/) by building a container, start it and execute a serie of tests to validate the correctness of the provisioned container.

2. Build a service and pack it into an image and deploy it to the docker registry.

3. Pack software as part of a deployment pipeline and deploy it to an IaaS, such as [Digital Ocean](https://www.digitalocean.com/).

You can expect a series of blogposts that cover these scenarios in detail soon.

### How to use docker on wercker

Your build and deployment pipeline is executed in a [wercker box](http://devcenter.wercker.com/articles/boxes/). A box is basically a virtual machine with a set of packages installed to support your stack of choice.

The box that has docker available is released under the *wercker-labs* account and can be used by setting the box element in your [wercker.yml](http://devcenter.wercker.com/articles/werckeryml/) to `wercker-labs/docker`. 

Here is an example that demonstrates a [wercker.yml](http://devcenter.wercker.com/articles/werckeryml/) which echos the docker version from within the build pipeline:

``` yaml
box: wercker-labs/docker
build:
  steps:
    - script:
        name: Build the application
        code: |
          docker -v
```

A wercker environment is immutable and every build and deploy is executed in a clean environment. To speed up the build process of your docker containers we've added the following base images to wercker which you can leverage:

* [ubuntu](https://index.docker.io/_/ubuntu/)
* [base](https://index.docker.io/_/base/)
* [busybox](https://index.docker.io/_/busybox/)
* [centos](https://index.docker.io/_/centos/)

Please let us know if you need any other base images!

### Other packages

The box runs ubuntu 13.04 (Raring Ringtail) and is packed with packages for all major development platforms including ruby, python, nodejs, php, openjdk, erlang and go. It also has development headers and clients installed for database services.

If you like to add extra packages, you can install them as part of your build or deployment pipeline with the [`install-packages`](https://app.wercker.com/#applications/51c829ea3179be4478002168/tab/details) step:

``` yaml
box: wercker-labs/docker
build:
  steps:
    - install-packages:
        packages: apache
    - script:
        name: Build the application
        code: |
          docker -v
```

If you think your packages should be part of the box, just let us know!

### Caveats

Here is a list of the caveats. We will continue working on fixing these and the priority is based on the voice of our users.

* wercker [services](http://devcenter.wercker.com/articles/services/) are not supported.
* You cannot inherit from the `wercker-labs/docker` box.
* The number of packages installed is limited. Please us know if you miss any!

### We are here to help!

As always, we are here to help your builds turn green and your software deployed. We're also looking forward to receive feedback. You can contact us by replying to this [e-mail](mailto:pleasemailus@wercker.com). You can request features or get support via [uservoice](http://wercker.uservoice.com/forums/181077-general).

### What is next?

We will continue to work on our Docker support. You can expect a number of articles that will explain common use-case scenarios plus internals.

## Earn some stickers!

Let us know about the applications you build with wercker. Don't forget to tweet out a screenshot of your first green build with **#wercker** and we'll send you some [@wercker](http://twitter.com/wercker) stickers.

Follow us on [twitter](http://twitter.com/wercker) as well to stay in the loop.
