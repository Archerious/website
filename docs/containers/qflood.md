<div class="image-logo"><img src="/img/image-logos/flood.svg" alt="logo"></div>

[:octicons-mark-github-16: GitHub](https://github.com/hotio/qflood){: .header-icons target=_blank rel="noopener noreferrer" }  
[:octicons-container-16: GitHub Registry](https://github.com/orgs/hotio/packages/container/package/qflood){: .header-icons target=_blank rel="noopener noreferrer" }  
[:material-docker:{: style="transform: scale(1.3);" } Docker Hub](https://hub.docker.com/r/hotio/qflood){: .header-icons target=_blank rel="noopener noreferrer" }  
[:octicons-link-16: qBittorrent](https://github.com/qbittorrent/qbittorrent){: .header-icons target=_blank rel="noopener noreferrer" }  
[:octicons-link-16: Flood](https://github.com/jesec/flood){: .header-icons target=_blank rel="noopener noreferrer" }  

--8<-- "includes/stats.md"

!!! question "What is this?"

    A docker image with qBittorrent and the Flood UI, also optional WireGuard VPN support.

## Starting the container

!!! docker ""

    === "cli"

        ```shell
        docker run --rm \
            --name qflood \
            -p 8080:8080 \
            -p 3000:3000 \
            -e PUID=1000 \
            -e PGID=1000 \
            -e UMASK=002 \
            -e TZ="Etc/UTC" \
            -e FLOOD_AUTH="false" \
            -v /<host_folder_config>:/config \
            hotio/qflood
        ```

    === "compose"

        ```yaml
        version: "3.7"

        services:
          qflood:
            container_name: qflood
            image: hotio/qflood
            ports:
              - "8080:8080"
              - "3000:3000"
            environment:
              - PUID=1000
              - PGID=1000
              - UMASK=002
              - TZ=Etc/UTC
              - FLOOD_AUTH=false
            volumes:
              - /<host_folder_config>:/config
        ```

    === "cli vpn"

        ```shell
        docker run --rm \
            --name qflood \
            -p 8080:8080 \
            -p 3000:3000 \
            -p 8118:8118 \
            -e PUID=1000 \
            -e PGID=1000 \
            -e UMASK=002 \
            -e TZ="Etc/UTC" \
            -e VPN_ENABLED="true" \
            -e VPN_LAN_NETWORK="" \
            -e VPN_CONF="wg0" \
            -e VPN_ADDITIONAL_PORTS="" \
            -e PRIVOXY_ENABLED="false" \
            -e FLOOD_AUTH="false" \
            -v /<host_folder_config>:/config \
            --cap-add=NET_ADMIN \
            --sysctl="net.ipv4.conf.all.src_valid_mark=1" \
            --sysctl="net.ipv6.conf.all.disable_ipv6=0" \
            hotio/qflood
        ```

    === "compose vpn"

        ```yaml
        version: "3.7"

        services:
          qflood:
            container_name: qflood
            image: hotio/qflood
            ports:
              - "8080:8080"
              - "3000:3000"
              - "8118:8118"
            environment:
              - PUID=1000
              - PGID=1000
              - UMASK=002
              - TZ=Etc/UTC
              - VPN_ENABLED=true
              - VPN_LAN_NETWORK
              - VPN_CONF=wg0
              - VPN_ADDITIONAL_PORTS
              - PRIVOXY_ENABLED=false
              - FLOOD_AUTH=false
            volumes:
              - /<host_folder_config>:/config
            cap_add:
              - NET_ADMIN
            sysctls:
              - net.ipv4.conf.all.src_valid_mark=1
              - net.ipv6.conf.all.disable_ipv6=0
        ```

In most cases you'll need to add additional volumes, depending on your own personal preference, to get access to your files.

--8<-- "includes/tags.md"

--8<-- "includes/wireguard.md"
