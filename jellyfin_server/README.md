# Jellyfin Server Configuration

## Ports
This table contains all configured ports in this deployment.

| # | Protocol | Usage |
| :----: | :----: | ---- |
| 8096 | TCP | http  |
| 8920 | TCP | https |
| 1900 | TCP | dlna  |
| 7359 | TCP | discovery|
 
## Configuration
If you want a simple carefree setup make sure to not uncomment the following section.
```
# - name: JELLYFIN_PublishedServerUrl 
#   valueFrom:
#     secretKeyRef:
#       name: jellyfin-secrets
#       key: SERVER_URL
```

## Documentation
Following Image was used for this setup: https://github.com/linuxserver/docker-jellyfin