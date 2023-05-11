# Jellyfin Setup Guide
This is an installation guide for an entire Jellyfin setup containing Sonarr, Radarr, Prowlarr, qBittorrent running on Ubuntu 18.04.
<br>

## Prerequisits
```Ensure you have root permissions to the system```
<br>

### Setup Portainer
Portainer can be installed and configured using the following guide. This guide includes the installation of docker and docker-compose.
https://docs.fuga.cloud/how-to-install-portainer-docker-ui-manager-on-ubuntu-20.04-18.04-16.04

After succesfull installation Portainer should be reachable under: http://192.168.1.134:9000/
<br>

## Jellyfin
### Installation
Installation Guide: https://jellyfin.org/docs/general/installation/linux/#debian <br>

After succesfull installation Jellyfin should be reachable under: http://192.168.1.134:8096/

### Configuration
<br>

## Sonarr
### Installation
Installation Guide: https://sonarr.tv/#downloads-v3-linux-ubuntu <br>

After succesfull installation Sonarr should be reachable under: http://192.168.1.134:8989/

### Configuration
<br>

## Radarr
### Installation
https://www.youtube.com/watch?v=g0GIz49N3J4
After succesfull installation Radarr should be reachable under: http://192.168.1.134:7878/

Add volume
- container ``/home/qbittorrent/Downloads``
- host: ``/home/qbittorrent/docker``

### Configuration
https://raw.githubusercontent.com/Qballjos/portainer_templates/master/Template/template.json
<br>

## Prowlarr
### Installation
After succesfull installation Prowlarr should be reachable under: http://192.168.1.134:9696/

### Configuration
<br>

## qBittorrent
### Installation
After succesfull installation qBittorrent should be reachable under: http://192.168.1.134:8080/

### Configuration
<br>


# Tips & Tricks

## Helpful Commands for Troubleshooting
```sudo systemctl (status/start/stop)```

# Applying all resources
kubectl create -n jellyfin
kubectl apply -f jellyfin_server/
kubectl apply -f prowlarr_server/
kubectl apply -f sonarr_server/
kubectl apply -f radarr_server/

# Deleting all resources
kubectl delete -f jellyfin_server/
kubectl delete -f prowlarr_server/
kubectl delete -f radarr_server/
kubectl delete -f sonarr_server/
kubectl delete -n jellyfin
