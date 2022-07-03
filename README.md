# Start service
To start the service, you need to download docker images. First of all, log in to access GitHub Packages

```bash
docker login ghcr.io
```
Enter the GitHub username and insert the token. Here you can look how generate github token https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token

## Upload images
To download images, simply run the following commands in the terminal

```bash
docker pull ghcr.io/warlus-hackathon/backend:v0.1.0
docker pull ghcr.io/warlus-hackathon/frontend:v0.1.0
docker pull ghcr.io/warlus-hackathon/worker:v0.1.1
```
or
```bash
docker pull ghcr.io/warlus-hackathon/backend:main & docker pull ghcr.io/warlus-hackathon/frontend:main & docker pull ghcr.io/warlus-hackathon/worker:main
```
## Setting up environment variables
For the service to work correctly, you need to correctly set the environment variables in the .env file. Example:
```env
# to create postgres in container
POSTGRES_PASSWORD=<password>
POSTGRES_USER=warlus
POSTGRES_DB=warlus

# used in application postgres
DB_URL=postgresql://warlus:<password>@db:5432/warlus

# server config
APP_ENDPOINT=http://backend:5001
APP_PORT=5001
APP_HOST=0.0.0.0

# aws config
AWS_ENDPOINT=http://minio:9000
AWS_ACCESS_KEY_ID=<key_id>
AWS_SECRET_ACCESS_KEY=<acces_key>
AWS_BUCKET_NAME_INPUT_IMAGES=input-images
AWS_BUCKET_NAME_OUTPUT_IMAGES=output-images
AWS_BUCKET_NAME_OUTPUT_CVS=output-cvs

# endpoint for backend
ENDPOINT=http://backend:5001/api/v1

# FRONTED
FRONT_PORT=5000
FRONT_HOST=0.0.0.0
FRONT_LOGLEVEL=DEBUG
```
## Containers start
### 1. First start
First of all you need create tables in data base. We start two containers "db" and "backend"
```bash
docker-compose up -d backend db
```
Then you must get into "backend" container shell, and start command to create tables
```bash
docker-compose exec backend bash
python -m backend.models
exit
```
Tables created. This steps you need do only in first start, next, the tables will be in containers their re-creation will not be required. But if you delete "db" container, you need repeat this way.\

Now we start other containers
```bash
docker-compose up -d
```
### 2. Following start
In the future, to start containers, you just need to enter command:
```bash
docker-compose up -d
```

## Containers logging
If need get some information from containers work you may look at containers logging
```bash
docker-compose logs --tail 10 -f db
```

## Containers stop
If you need stop all containers:
```bash
docker-compose stop
```
If you need stop one of "db", "minio", "frontend", "baackend",  "worker" containers:
```bash
docker-compose stop db
```

## Containers delete/drop
If you need drop all containers:\
!!! NOTE - this command drop all your data in your containers.
```bash
docker-compose down
```


If you need drop one of "db", "minio", "frontend", "baackend",  "worker" containers:
```bash
docker-compose dawn backend
```
