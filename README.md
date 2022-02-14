# trident-iscsi

## Overview
Client iscsi utils installation for BOSH stemcells used by VMware TKGI (aka PKS enterprise).
Version 1.1 tested on ubuntu-xenial-621.208 stemcell.

## Installation

First login to bosh and set the environment variables. (Can be taken from OpsManager- BOSH Director Tile -> Credentials Tab -> Bosh Commandline Credentials) 

Download and Extract the installation file
~~~~
https://github.com/natke889/trident-iscsi/releases/download/1.1/trident-iscsi-v1.1-ubuntu-xenial-621.208.tar.gz

tar -zxvf trident-iscsi-v1.1-ubuntu-xenial-621.208.tar.gz
~~~~

Upload the addon release to bosh.
~~~~
bosh upload-release ./trident-iscsi-release.tgz
~~~~

Update bosh config with the new addon release.
~~~~
bosh -n update-config --name=trident-iscsi-addon --type=runtime ./trident-iscsi-addon.yml
~~~~

Applying to kubernetes cluster by upgrade errand
~~~~
bosh -n -d `bosh deployments | grep pivotal-container-service | head -1 | awk '{print $1}'` run-errand upgrade-all-service-instances
~~~~
