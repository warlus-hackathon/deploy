# Start service
To start the service, you need to download docker images. First of all, log in to access GitHub Packages

```bash
docker login ghcr.io
```
Enter the GitHub username and insert the token. Here you can look how generate github token https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token

## Upload images
To download images, simply run the following commands in the terminal

```bash
docker pull ghcr.io/warlus-hackathon/backend:main
docker pull ghcr.io/warlus-hackathon/frontend:main
docker pull ghcr.io/warlus-hackathon/worker:main
```
or
```bash
docker pull ghcr.io/warlus-hackathon/backend:main & docker pull ghcr.io/warlus-hackathon/frontend:main & docker pull ghcr.io/warlus-hackathon/worker:main
```
## Setting up environment variables
For the service to work correctly, you need to correctly set the environment variables in the .env file. Example:
```env

```
## Start service
You can use one of ways:
```bash
docker-compose up -d
```

# create tables in DB
```bash
docker-compose exec backend bash
python -m backend.models
exit
```