# Docker-Pihole-Unbound

Pi-hole container using the recursive DNS server unbound.<br/>
Enable in Pi-hole by setting custom DNS server to 127.0.0.1#5335

Check if unbound is running:<br/>
docker exec pihole s6-svstat /var/run/s6/services/unbound

Based on:<br/>
<a href="https://hub.docker.com/r/pihole/pihole">pihole/pihole</a><br/>
<a href="https://docs.pi-hole.net/guides/dns/unbound/">Unbound</a>

Example Usage:<br/>
sudo docker run -d --network host --name pihole-unbound --restart unless-stopped \
-p 53:53/tcp \
-p 53:53/udp \
-p 67:67/udp \
-p 80:80/tcp \
-p 443:443/tcp \
-v ${VOLUME}/etc-dnsmasq.d:/etc/dnsmasq.d \
-v ${VOLUME}/etc-pihole:/etc/pihole \
-v ${VOLUME}/etc-unbound:/etc/unbound \
-e "TZ=${TZ}" \
-e "WEBPASSWORD=${WEBPASSWORD}" \
-e "ServerIP=${ServerIP}" \
-e "DNS_BOGUS_PRIV=${DNS_BOGUS_PRIV}" \
-e "DNS_FQDN_REQUIRED=${DNS_FQDN_REQUIRED}" \
-e "DNSMASQ_LISTENING=${DNSMASQ_LISTENING}" \
-e "REV_SERVER=${REV_SERVER}" \
-e "REV_SERVER_DOMAIN=${REV_SERVER_DOMAIN}" \
-e "REV_SERVER_TARGET=${REV_SERVER_TARGET}" \
-e "REV_SERVER_CIDR=${REV_SERVER_CIDR}" \
-e "DNS1=127.0.0.1#5335" \
-e "DNS2=127.0.0.1#5335" \
-e "WEB_PORT=${WEB_PORT}" \
pihole-unbound:latest
