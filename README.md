# Jellyfin Setup Guide
This is an installation guide for a containerized Jellyfin Stack available for Kubernetes.
<br>

## Prerequisits
This guide assumes that you have setup your cluster on Ubuntu 18.04 nodes.
```"Please ensure you have root permissions to the system"```
### Setup qBittorrent
Follow this guide to install qBittorrent on Ubuntu 18.04:
[Install Guide](https://www.linuxbabe.com/ubuntu/install-qbittorrent-ubuntu-18-04-desktop-server)

connecting your downloader to Radarr & Sonarr is no harder then connecting over localhost:8080 or the respective IP-Adresse of the Server hosting your qBittorrent installation. <br>
> security: when possible use dedicated credentials to authenticate to your torrent client.

## Jellyfin


## Sonarr & Radarr
Both applications have a near identical UI and require the same configuration steps. Keep in mind Sonarr is used for Series whereas Radarr is used for Movies.

### Adding Downlaod Client
To add a download client switch to Settings/Download Clients add your selected torrent client. <br>
> security: when possible use dedicated credentials to authenticate to your torrent client.

## Prowlarr
To connect Radarr & Sonarr under Settings/Apps add the following two applications with this configuration
- Prowlarr Server: http://prowlarr-service:9696
- Radarr Server: http://radarr-service:7878
- Sonarr Server: http://sonarr-service:8989

ApiKeys for both Applications can be found in the respective UI under Settings/General.


## Applying all resources
kubectl create ns jellyfin <br>
kubectl apply -f jellyfin_server/ <br>
kubectl apply -f prowlarr_server/ <br>
kubectl apply -f sonarr_server/ <br>
kubectl apply -f radarr_server/ <br>

## Deleting all resources
kubectl delete -f jellyfin_server/ <br>
kubectl delete -f prowlarr_server/ <br>
kubectl delete -f radarr_server/ <br>
kubectl delete -f sonarr_server/ <br>
kubectl delete ns jellyfin <br>


## Security
### Network Policies
Following communication is allowed by default further communication will require you to edit the network policies. More information can be found under: [Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

| Type | Start | End | Port | Protocol | 
|------|-------|-----|------|----------|
| Ingress | radarr-service | jellyfin-service | 7878 | tcp
| Ingress | sonarr-service | jellyfin-service | 8989 | tcp
| Egress  | jellyfin-service | radarr-service | 7878 | tcp
| Egress  | jellyfin-service | sonarr-service | 8989 | tcp

## Troubleshooting
### No Disk Space
Should you encounter a jammed disk switch to your root directory and from there run the command ```sudo du -xd 1``` keep doing so until you reach the directory jamming your system and ensure you delete it properly by running ```sudo rm -rf /dir```

### Test Pod
To run the test-pod use following command: 
```kubectl apply -f test-pod.yaml``` <br>
To test functionality of network policies you can run the test-pod and use the curl command: 
```curl component-service:port``` <br>