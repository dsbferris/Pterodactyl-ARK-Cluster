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
### Create Directories on host
```
sudo mkdir -p /var/lib/pterodactyl/mounts/ark/cluster-dir
sudo mkdir -p /var/lib/pterodactyl/mounts/ark/server-files/ShooterGame/Content
```

### Import the modified Egg
Click on Nests and import this modified egg.  
You might want to create your own Nest for this.

### Create Mounts in Panel
Default settings.

- Ark Cluster Dir /var/lib/pterodactyl/mounts/ark/cluster-dir/ /mnt/ark/cluster-dir/
- Ark ShooterGame Content /var/lib/pterodactyl/mounts/ark/server-files/ShooterGame/Content/ /mnt/ark/server-files/ShooterGame/Content/

Add Node and Egg to each mounts.

### Create New Server
- Set Name and Owner.
- Disable "Start Server when installed"!
- You need 4 Port allocations.
    - 1. GamePort, default 7777
    - 2. GamePort UDP, will always be GamePort+1
    - 3. QueryPort, default 27015, this one you will connect to via Server Browser or Server Favourites
    - 4. RCONPort, default 27020, needed internally and can used with e.g. ARKon
    - But I personally prefer allocation 27001-270XX and use 01, 02 for GamePort, 03 for Query and 04 for RCON.
- Set the Default Allocation to 27001, Select 27002, 27003, 27004 in Additional Allocations.
- Set Memory and Diskspace to 0.
- Select the Egg.
- Set Server and Admin Password.
- Set Map and Name.
- Set the Query Port to 27003 and RCON Port to 27004.
- Auto-update must be enabled for the first time your start!!!
- Set ClusterID.
- Set Cluster Dir to /mnt/ark/cluster-dir/
- Set Install Dir to /mnt/ark/server-files/
- Set everything else to your needs.
- Click Create Server.

### Add Mount to Server
After the server finished installing, usually a few seconds, do the following:
- Click on the left to Servers and select your freshly created Server.
- Click on mounts and click the + to mount all previously defined mounts.

### Finished
Now you can go the Panel, the Icon that looks like Export, and start up your server.
The whole game will be downloaded (around 20GB) on your first start.
I recommend letting the first server finish before creating and starting another server.
Each additional server will use the ShooterGame/Content from the first one, so you save a whooping 18GB in download and storage! Yay!

Multiple Server can now share the ClusterDir to successfully make a cluster.

### Uninstall
If you want to get rid of all your Ark Servers and the Storage occupied by them do the following:
- Delete all ark servers
- Delete the mounts
- Delete the mounts directory on the host: `sudo rm -rf /var/lib/pterodactyl/mounts/ark`