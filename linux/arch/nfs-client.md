# Set up NFS client
See here: https://project.altservice.com/issues/645

## Mount the NFS Share

Install nfs-utils package:

`sudo pacman -S nfs-utils`

Start and enable rpcbind.service,nfs-client.target and remote-fs.target services at boot:

    sudo systemctl enable rpcbind.service
    sudo systemctl enable nfs-client.target
    sudo systemctl enable remote-fs.target

    sudo systemctl start rpcbind.service
    sudo systemctl start nfs-client.target
    sudo systemctl start remote-fs.target

