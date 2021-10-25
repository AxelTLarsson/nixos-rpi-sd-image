# nixos-rpi-sd-image

A convenient way to create custom Raspberry Pi NixOS SD images.

❕ **N.B!** Use this to bootstrap the raspberry pi - just to get a basic system working! Then move onto my dotfiles/nixpi/configuration.nix.

So far this has been tested to work with Docker Desktop for Mac and also Docker
on Linux.

## Setup

1.  Install QEMU into the host machine:

    ```sh
    docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
    ```

2.  Clone this repo.

3.  Configure `nixos-rpi-sd-image/sd-image.nix` and
    `nixos-rpi-sd-image/configuration.nix` with your own settings.

## Run

1.  Use `docker-compose` to mount `output` and run the container:

    ```sh
    docker-compose up
    ```

2.  Check the `output` directory for the `.img` file.

## SD Image Usage

1.  Burn the `.img` file in `output` to an SD card with your preferred method.

2.  Insert the SD card into the Raspberry Pi and wait for it to boot.

3.  Wait for NixOS to rebuild and switch (this may take a long time) or SSH into
    the Raspberry Pi, then run the following command to monitor progress:

    ```sh
    journalctl -f -u sd-image-init.service
    ```

4.  Manually remove the inclusion of ./sd-image-init.nix in /etc/nixos/configuration.nix otherwise changes will be lost on reboot.
5.  Enjoy!

## Credit

This was possible mostly in part because of the blog posts and code of
[@Robertof][], but also the contributors to `nixos-generators` and the wiki for
NixOS on ARM.

[NixOS on ARM > Building your own image > Compiling through QEMU][]

[NixOS on a Raspberry Pi: creating a custom SD image with OpenSSH out of the box by @Robertof][]

[NixOS Docker-based SD image builder][]

[nixos-generators - one config, multiple formats][]

[@robertof]: https://github.com/Robertof
[nixos on arm > building your own image > compiling through qemu]: https://nixos.wiki/wiki/NixOS_on_ARM#Compiling_through_QEMU
[nixos on a raspberry pi: creating a custom sd image with openssh out of the box by @robertof]: https://rbf.dev/blog/2020/05/custom-nixos-build-for-raspberry-pis/
[nixos docker-based sd image builder]: https://github.com/Robertof/nixos-docker-sd-image-builder
[nixos-generators - one config, multiple formats]: https://github.com/nix-community/nixos-generators
