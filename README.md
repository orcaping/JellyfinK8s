# Jellyfin Setup Guide
This is an installation guide for an entire Jellyfin setup containing Sonarr, Radarr, Prowlarr, qBittorrent running on Ubuntu 18.04.
<br>

## Prerequisits
```Ensure you have root permissions to the system```
### Setup qBittorrent
Follow this guide to install qBittorrent on Ubuntu 18.04.
https://www.linuxbabe.com/ubuntu/install-qbittorrent-ubuntu-18-04-desktop-server

connecting your downloader to Radarr & Sonarr is no harder then connecting over localhost:8080 or the respective IP-Adresse of the Server hosting your qBittorrent installation. <br>
```security: when possible use dedicated credentials to authenticate to your torrent client.```

## Jellyfin


## Sonarr & Radarr
Both applications have a near identical UI and require the same configuration steps. Keep in mind Sonarr is used for Series whereas Radarr is used for Movies.

### Adding Downlaod Client
To add a download client switch to Settings/Download Clients add your selected torrent client. <br>
```security: when possible use dedicated credentials to authenticate to your torrent client.```

## Prowlarr
To connect Radarr & Sonarr under Settings/Apps add the following two applications with this configuration
- Prowlarr Server: http://prowlarr-service:9696
- Radarr Server: http://radarr-service:7878
- Sonarr Server: http://sonarr-service:8989

ApiKeys for both Applications can be found in the respective UI under Settings/General.


# Applying all resources
kubectl create ns jellyfin <br>
kubectl apply -f jellyfin_server/ <br>
kubectl apply -f prowlarr_server/ <br>
kubectl apply -f sonarr_server/ <br>
kubectl apply -f radarr_server/ <br>

# Deleting all resources
kubectl delete -f jellyfin_server/ <br>
kubectl delete -f prowlarr_server/ <br>
kubectl delete -f radarr_server/ <br>
kubectl delete -f sonarr_server/ <br>
kubectl delete ns jellyfin <br>


# Scan for Vulnerabilites
/Users/mainuser/go/bin/kubesec scan xx.yaml