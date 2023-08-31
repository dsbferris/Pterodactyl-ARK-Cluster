# How to Cluster

### Build customized docker container
`bash build.sh`

### Wings config.yml
```
...
allowed_mounts:
- /var/lib/pterodactyl/mounts
...
```
### Create Directories on wings host
```
sudo mkdir -p /var/lib/pterodactyl/mounts/ark/cluster-dir/clusters
sudo mkdir -p /var/lib/pterodactyl/mounts/ark/server-files/ShooterGame/Content
sudo chown 988:988 -R /var/lib/pterodactyl/mounts/ark/cluster-dir/clusters
sudo chown 988:988 -R /var/lib/pterodactyl/mounts/ark/server-files/ShooterGame/Content
```

### Import the modified Egg
Click on Nests and import this modified egg.  
You might want to create your own Nest for this.

### Create Mounts in Panel
Default settings.

- Ark Cluster Dir /var/lib/pterodactyl/mounts/ark/cluster-dir/ /mnt/ark/cluster-dir/
- Ark ShooterGame Content /var/lib/pterodactyl/mounts/ark/server-files/ShooterGame/Content/ /mnt/ark/server-files/ShooterGame/Content/

Add Node and Egg to each mounts.
