
# NFS Setup
https://wiki.ubuntuusers.de/NFSv4/
## Server Setup
```
sudo apt install nfs-kernel-server  -y
sudo cat /proc/fs/nfsd/versions 
# Output: +3 +4 +4.1 +4.2
sudo mkdir -p /srv/nfsv4/arkcluster
mkdir /home/$USER/arkcluster
printf "/home/$USER/arkcluster        /srv/nfsv4/freigabe1  none  bind  0 0\n" | sudo tee -a /etc/fstab
printf "/srv/nfsv4   192.168.178.0/24(rw,sync,root_squash,no_subtree_check,fsid=0)\n/srv/nfsv4/arkcluster  192.168.178.0/24(rw,sync,root_squash,no_subtree_check)\n" | sudo tee -a /etc/exports
sudo service nfs-kernel-server reload 
sudo exportfs -v 
```

## Client Setup
```
sudo apt install nfs-common -y
sudo mkdir -p /mnt/nfsv4-client/arkcluster
sudo mount -t nfs -o nfsvers=4,minorversion=2 192.168.178.2:/arkcluster /mnt/nfsv4-client/arkcluster
mount 
```

Check if works! Create some files, delete some files.
```
printf "192.168.178.2:/arkcluster /mnt/nfsv4-client/arkcluster nfs nfsvers=4,minorversion=2,rw 0 0\n" | sudo tee -a /etc/fstab
```

## IMPORTANT!
Ensure correct ownership!

mkdir /mnt/nfsv4-client/arkcluster/clusters
sudo chown 988:988 /mnt/nfsv4-client/arkcluster/clusters

# Pterodactyl Setup

### Build customized docker container
`bash build.sh`

### Wings config.yml
```
...
allowed_mounts:
- /var/lib/pterodactyl/mounts
- /mnt/nfsv4-client/arkcluster
...
```
### Create Directory on wings host
```
sudo mkdir -p /var/lib/pterodactyl/mounts/ark/server-files/ShooterGame/Content
sudo chown 988:988 -R /var/lib/pterodactyl/mounts/ark/server-files/ShooterGame/Content
```

### Import the modified Egg
Click on Nests and import this modified egg.  
You might want to create your own Nest for this.

### Create Mounts in Panel
Default settings.

- Ark NFS Cluster Dir /mnt/nfsv4-client/arkcluster/ /mnt/ark/cluster-dir/
- Ark ShooterGame Content /var/lib/pterodactyl/mounts/ark/server-files/ShooterGame/Content/ /mnt/ark/server-files/ShooterGame/Content/

Add Node and Egg to each mounts.
