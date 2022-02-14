# trident-iscsi

bosh upload-release ./iscsi-1.5.tgz

# Apply the addon in a way that ops man won't overwrite it:
bosh -n update-config --name=iscsi-addon --type=runtime ./pks-manifest.yml

# Then to add this to all existing kubernetes clusters, just re-run the upgrade errand

# bosh -n -d `bosh deployments | grep pivotal-container-service | head -1 | awk '{print $1}'` run-errand upgrade-all-service-instances
