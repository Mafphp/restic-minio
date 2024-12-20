# Restic Backup and Restore with Docker Compose

This project sets up a backup and restore system using Restic and Docker Compose. Restic is a fast, secure, and efficient backup tool, and this configuration simplifies its usage with Docker containers.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Features](#features)
3. [Prerequisites](#prerequisites)
4. [Environment Variables](#environment-variables)
5. [Usage](#usage)
    - [Run Shell in Restic Container](#run-shell-in-restic-container)
    - [Backup](#backup)
    - [Restore](#restore)

---

## Introduction

This project enables automated and manual backups of Docker volumes to a remote S3-compatible storage (e.g., MinIO). Restic manages the backups, retention policies, and restores with ease.

---

## Features

- Automated backups with retention policies for daily, weekly, and monthly snapshots.
- Secure storage of backup data with encryption.
- Support for S3-compatible storage services like MinIO, AWS S3, and others.
- Easily restore backups to target directories.

---

## Prerequisites

- Docker and Docker Compose installed.
- An S3-compatible storage service (e.g., MinIO) configured and accessible.
- Ensure the Docker volume `sm-wp_db_data` exists and is external.

---

## Environment Variables

Create a `.env` file in the root of your project with the following values:

```env
RESTIC_REPOSITORY=s3:http://<minio-server>:9000/<bucket-name>
RESTIC_PASSWORD=yourpasswordhere
AWS_ACCESS_KEY_ID=your-access-key-id
AWS_SECRET_ACCESS_KEY=your-secret-access-key
```

## Run Shell in Restic Container
```script
docker compose run --rm --entrypoint /bin/sh restic-backup
```
for old version of docker-compose
```script
docker-compose run --rm --entrypoint /bin/sh restic-backup
```
## Backup
```script
docker compose run --rm --entrypoint /bin/sh restic-backup
```
for old version of docker-compose
```script
docker-compose up -d
```
## Restore
```script
docker-compose run restic-restore restic restore --target /backup/restore
```
for old version of docker-compose
```script
docker-compose run restic-restore restic restore --target /backup/restore
```


```
docker compose run --rm restic backup /backup
docker compose run --rm restic snapshots
docker compose run --rm restic diff  39a5119c  39229572
docker compose run --rm restic forget --keep-daily 7 --keep-weekly 4 --keep-monthly 12 --prune
```
