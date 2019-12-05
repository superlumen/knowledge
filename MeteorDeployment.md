Last update: August 2017

tl;dr

* mup
* backup mongo from docker

## Deployment

mup has switched maintainers and seems to be under active development as at 1 Aug 2017.

## Backup

mup will install docker and spin up 1 container for mongo and 1 for each meteor app.

The `mongodb` container gets the host path `/var/lib/mongdb/` mounted at `/data/db/` and that's where the mongo data lives. However, we can't directly back that up. Instead, run these commands from the host:

```bash
docker exec -it mongodb mongodump --archive=/root/mongodump.gz --gzip
docker cp mongodb:/root/mongodump.gz /backup/mongo/mongodump_$(date +%Y-%m-%d_%H-%M-%S).gz
```

That dumps a gzip compressed backup file (of all databases) to `/root/mongodump.gz` inside the container. Then the second line copies that from the container to `/backup/mongo/` on the host. You can automate this from cron, and further automate the backup of your `/backup/` folder as well.
