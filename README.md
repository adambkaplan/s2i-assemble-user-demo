# s2i-assemble-user-demo
Demo of s2i builders with assemble-user overrides.

## Images
This repository contains two s2i builder Docker image specs:

1. s2i-normal - an s2i builder with an unprivileged user as the assemble user override
2. s2i-root - an s2i builder with root as the assemble user override

## Manifests
The following manifests are included to demonstrate OpenShift security features with s2i builds, under `manifests/openshift`:

1. demo-is.yaml - set up `ImageStreams` for the builder images and s2i build output.
2. demo-*-build-bc.yaml - build configurations for the `s2i-root` and `s2i-normal` builder images.
3. demo-*-s2i-bc.yaml - build configurations demonstrating an s2i build using the above builder images.

## Running the demo

### Requirements

1. An OpenShift cluster running v3.10.0 or higher
2. Setup the build image streams:
```
$ oc create -f manifest/openshift/demo-is.yaml
```
3. Create the builder images
```
$ oc create -f demo-normal-build-bc.yaml
...
$ oc start-build demo-normal-build --follow
...
$ oc create -f demo-root-build-bc.yaml
...
$ oc start-build demo-root-build --follow
...
```
### Demo
1. Create and run the normal build - this should succeed.
```
$ oc create -f demo-normal-s2i-bc.yaml
...
$ oc start-build demo-normal-s2i --follow
...
```
2. Create and run the root build - this should fail with an error.
```
$ oc create -f demo-root-s2i-bc.yaml
...
$ oc start-build demo-root-s2i --follow
...
```
