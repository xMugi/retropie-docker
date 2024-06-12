# retropie-docker
Docker resources to run Retropie Install script as a container, and game using Retropie on Linux without the need of dual-boot

Note that it is implicit that you might need to have docker daemon already running, or any additional software that is capable of handling docker images like `podman`(`podman-docker` might also be handy to help with cli syntax)

Install the `xhost` command on your desktop as well.

# How to build the image

    git clone --depth=1 https://github.com/xMugi/retropie-docker.git
    cd retropie-docker
    docker build -t retropie-docker .

This will build an image that is currently based on Ubuntu LTS 20.04 from official docker images because, this is a requisite for Retropie. Needs further testing if this could be done with a Debian image as well.

Ubuntu 22.04 is not supported due to an SDL2 bug that is making retroarch autoconfiguraton steps break.

# Running a container instance of this image

Take a look at the `cmd.sh` file from this repo, and change the directories to one that will better reflect the location you want to keep your Roms, BIOS, User local EmulationStation dir (`es_homedir_config`), Global Emulationstation config (`es_config`) and Retroarch autogenerated controler files(`retroarch_autoconfig`).

These are pretty much the places you need to keep on your home directory after kill out your container.

To run:

    $ chmod +x cmd.sh
    $ ./cmd.sh

If you have first started EmulationStation, it will clean-up all controller config data as per `entrypoint.sh`. After that, EmulationStation will be launched. `cmd.sh` script will also set the permissions for the docker process to access X with the `xhost` utility.

# Currently known issues

So far, you'll have to map your local paths inside `cmd.sh` while we develop something like a config file.
