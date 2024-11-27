docker-compose run --rm --entrypoint /bin/sh restic-backup
 
docker-compose run restic-backup restic restore --target /backup/restore

docker compose run restic-backup restic restore --target /backup/restore
