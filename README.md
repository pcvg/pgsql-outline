# pgsql-outline
PostgreSQL Docker image with Outline VPN

## Interactive container launch

```bash
docker run -it \
  --network host \
  --privileged \
  --cap-add NET_ADMIN \
  --cap-add SYS_MODULE \
  --device /dev/net/tun:/dev/net/tun \
  -e VPN_CONFIG="OUTLINE_SS_LINK" \
  -e PGHOST="192.168.2.1" \
  -e PGDATABASE="postgres" \
  -e PGUSER="postgres" \
  -e PGPASSWORD="best_pAs5_in_the_W0rld" \
  -v ./volume_for_dump:/tmp/volume_for_dump \
  savingsutd/pgsql-outline:latest \
  bash -c "proxychains4 pg_dump -p 5432 --format=custom --compress=9 --verbose --no-owner --no-privileges --file=/tmp/volume_for_dump/db.dump"
```
