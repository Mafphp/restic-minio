
docker-compose run --rm --entrypoint /bin/sh restic-backup


backup: 
docker-compose up -d
docker compose up -d

restore:
docker-compose run restic-restore restic restore --target /backup/restore
docker compose run restic-restore restic restore --target /backup/restore
