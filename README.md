# opx-build

This repository contains build information for OpenSwitch OPX Base.

## Quick Start

Requires [`docker`](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/), [`repo`](https://source.android.com/source/downloading), and `git`.

```bash
# Clone repositories
repo init -u git://git.openswitch.net/opx/opx-manifest && repo sync

# Build docker image
pushd opx-build/scripts
./opx_setup
popd

# Build all repositories
./opx-build/scripts/opx_run -ci "cd /mnt && opx-build/scripts/opx_build"
```

## Get OpenSwitch Base
There are two ways to get the image:
- **Download and install binaries** — see Installation below for complete information, **or**
- **Build from scratch** — see the step-by-step instructions below to build the project.

## Build environment recommendations
- Intel multi-core
- Ubuntu 16.04 or later (desktop edition with Python installed)
- 20G available free disk space

## Build environment prerequisites
Updated environment: `sudo apt-get update`
- GIT: `sudo apt-get install git`
- Repo: `sudo apt-get install repo`
- apt-utils: `sudo apt-get install apt-utils`
- Docker: `sudo apt-get install docker.io`

## Clone the source code
To get the source files for the OpenSwitch OPX Base repositories, run the commands in an empty directory (root directory). For example: _~/dev/opx/_:

    repo init -u https://github.com/open-switch/opx-manifest.git
    repo sync

The `repo sync` command downloads all of the source files that you need to build OpenSwitch. In addition to the source files, you will also need some binary libraries for the SAI. The SAI is currently not open sourced entirely, as it is based on Broadcom's SDK and there is no open source SAI implementation from Broadcom at this time.

All build scripts are found in the `opx-build` repo and will be downloaded as part of the above `repo sync`.

## Build the code
Setup your path to include _opx-build/scripts_ folder (if you plan to run this command often, you could optionally add it to the `.bashrc`):

    cd opx-build/scripts
    export PATH=$PATH:$PWD

## OpenSwitch Docker environment
To setup your Docker OPX image, use the script in the _opx-build/scripts_ folder called `opx_setup`. This script builds a Docker container called `docker-opx` which will be used by the build scripts:

    cd opx-build/scripts/
    ./opx_setup

## Build one repository
Go to the root directory where you installed the OPX repositories and run the OPX Docker container:

    cd ~/dev/opx
    opx-build/scripts/opx_run

To build a single repository, go to the repository and build. For example, to build `opx-logging`:

    opx-dev@077f7b30f8ef:/# cd /mnt
    opx-dev@077f7b30f8ef:/mnt# opx-build/scripts/opx_build opx-logging

## Build all repositories
Issue the `opx_build all` command from the root directory to build all repos and create packages in the same root directory.

    opx-dev@077f7b30f8ef:/# cd /mnt
    opx-dev@077f7b30f8ef:/mnt# opx-build/scripts/opx_build all

## Installation
Once all of the repositories have been built, you can install the created ONIE Debian x86_64 image. You can then install all of the build packages, along with other Debian files you downloaded earlier in the root directory.

See [Install OpenSwitch OPX Base on Dell S6000 Platform](https://github.com/open-switch/opx-docs/wiki/Install-OPX-Base-on-Dell-S6000-ON-platform) for complete information.

(c) 2017 Dell
