# Docker-Pihole-Unbound

Pi-hole container using the recursive DNS server unbound.<br/>
Enable in Pi-hole by setting custom DNS server to 127.0.0.1#5335

Check if unbound is running:<br/>
docker exec pihole s6-svstat /var/run/s6/services/unbound

Based on<br/>
<a href="https://hub.docker.com/r/pihole/pihole">pihole/pihole</a><br/>
<a href="https://docs.pi-hole.net/guides/dns/unbound/">Unbound</a>

Example Usage<br/>
sudo docker run -d --network host --name pihole-unbound --restart always \
-p 53:53/tcp \
-p 53:53/udp \
-p 67:67/udp \
-p 80:80/tcp \
-p 443:443/tcp \
-v /volume1/docker/pihole/etc-dnsmasq.d:/etc/dnsmasq.d \
-v /volume1/docker/pihole/etc-pihole:/etc/pihole \
-v /volume1/docker/pihole/etc-unbound:/etc/unbound \
-e "TZ=Europe/Berlin" \
-e "WEBPASSWORD=PASSWORD" \
-e "ServerIP=192.168.178.60" \
-e "REV_SERVER=true" \
-e "REV_SERVER_DOMAIN=fritz.box" \
-e "REV_SERVER_TARGET=192.168.178.1" \
-e "REV_SERVER_CIDR=192.168.178.0/24" \
-e "DNS1=127.0.0.1#5335" \
-e "DNS2=127.0.0.1#5335" \
-e "WEB_PORT=8081" \
pihole-unbound:latest
