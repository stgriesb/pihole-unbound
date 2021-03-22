# Docker-Pihole-Unbound

Pi-hole container using the recursive DNS server unbound.

Enable in Pi-hole by setting custom DNS server to 127.0.0.1#5353

Check if unbound is running:

docker exec pihole s6-svstat /var/run/s6/services/unbound

Based on

    pihole/pihole
    Unbound

Example Usage

docker create \
--name pihole \
-p 53:53/tcp -p 53:53/udp \
-p 80:80 \
-p 443:443 \
-e TZ=Europe/Berlin \
-e WEBPASSWORD:password \
-e ServerIP=192.168.178.60 \
-e IPv6=false \
-e REV_SERVER: "true" \
-e REV_SERVER_DOMAIN: "fritz.box" \
-e REV_SERVER_TARGET: "192.168.178.1" \
-e REV_SERVER_CIDR: "192.168.178.0/24" \
-e DNS1=127.0.0.1#5353 \
-e DNS2=127.0.0.1#5353 \
-v "$(pwd)/etc-pihole/:/etc/pihole/" \
-v "$(pwd)/etc-dnsmasq.d/:/etc/dnsmasq.d/" \
-v "$(pwd)/etc-unbound/:/etc/unbound/" \
--net=host \
--restart=unless-stopped \
stgriesb/pihole-unbound:latest
