# canvas/base-image-iso

This is a base image for canvas built from an Ubuntu ISO.

## Build
Unfortunatelly virtualbox images cannot be built on CI Services due to limitations on nested virtualization. 
So here are the steps needed to build the build the images locally.

```shell script
packer validate
packer build packer.json
```