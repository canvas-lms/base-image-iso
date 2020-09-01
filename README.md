# canvas/base-image-iso

This is a base image for canvas built from an Ubuntu ISO. However it is not really canvas specific but contains just 
a minimal ubuntu install. 

# Usage
Prebuilt images (`*.ova` for virtualbox and `*.box` for vagrant) are available at 
[Github](https://github.com/canvas-lms/base-image-iso/releases). See the Build section for instructions on
building locally.

## As a base image for packer
The image can be used as a base image for packer to build onto. For details also see 
[canvas/base-image-ova](https://github.com/canvas-lms/base-image-ova)

```json
// Insert packer.json
```

## As a Vagrant box
```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "../../canvas-org/base-image-iso/dist/packer-ubuntu64.box"
  config.ssh.username = "ubuntu"
  config.ssh.password = "ubuntu"
  
  # The box comes without the guest additions installed so default mounting with vboxfs would fail. 
  # You can install the guest additions your self, use the vagrant-vbguest plugin (https://github.com/dotless-de/vagrant-vbguest)
  # or choose rsync or smb sync.
  config.vm.synced_folder ".", disabled: true
end

```

## As a standalone virtualbox vm
The image can also be used to create a virtual machine without vagrant, just open the `.ova` file with virtualbox.

# Build
Unfortunatelly virtualbox images cannot be built on CI Services due to limitations on nested virtualization. 
So here are the steps needed to build the images locally.

```shell script
packer validate packer.json
packer build packer.json
```

