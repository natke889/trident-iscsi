# trident-iscsi

## Overview
Client iscsi utils installation for BOSH stemcells used by VMware TKGI (aka PKS enterprise).
Version 1.1 tested on ubuntu-xenial-621.208 stemcell.

## Installation

First login to bosh and set the environment variables. (Can be taken from OpsManager- BOSH Director Tile -> Credentials Tab -> Bosh Commandline Credentials) 

Upload the addon release to bosh.
~~~~
...
bosh upload-release ./trident-iscsi-v1.1-ubuntu-xenial-621.208.tgz
...
~~~~

Update bosh config with the new addon release.
~~~~
bosh -n update-config --name=trident-iscsi-addon --type=runtime ./trident-iscsi-addons.yml
~~~~

Applying to kubernetes cluster by upgrade errand
~~~~
bosh -n -d `bosh deployments | grep pivotal-container-service | head -1 | awk '{print $1}'` run-errand upgrade-all-service-instances
~~~~
