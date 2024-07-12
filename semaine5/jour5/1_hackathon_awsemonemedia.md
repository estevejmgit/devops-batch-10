```
version: '3.5'

services:
  jellyfin:
    image: "jellyfin/jellyfin:latest"
    container_name: jellyfin
    user: 1000:1000
    network_mode: 'host'
    volumes:
      - ./config:/config
      - ./cache:/cache
      - type: bind
        source: ./media
        target: /media
    restart: 'unless-stopped'

  deluge:
    image: linuxserver/deluge
    container_name: deluge
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Paris # Changez le fuseau horaire si nécessaire
    volumes:
      - ./deluge-config:/config
      - ./media:/downloads
    ports:
      - 8112:8112   # Port pour l'interface web de Deluge
      - 58846:58846 # Port pour le daemon Deluge
      - 58946:58946/udp # Port pour les connexions entrantes des torrents
    restart: unless-stopped

  jackett:
    image: linuxserver/jackett
    container_name: jackett
    environment:
      - PUI=1000
      - PGID=1000
      - TZ=Europe/Paris # Changez le fuseau horaire si nécessaire
    volumes:
      - ./jackett-config:/config
      - ./media:/downloads
    ports:
      - 9117:9117
    restart: unless-stopped
```
