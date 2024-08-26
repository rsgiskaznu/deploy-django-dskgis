# Instructions for deploying `django-dskgis` 


Pre-requisites:
- Docker installed on your machine
- Docker compose installed on your machine
- Git installed on your machine
- Your machine should have a stable internet connection, and it should be able to ping `cr.azat.host` and `docker.io`

Steps to deploy:

1. Clone the repository:
```bash
git clone https://github.com/azataiot/deploy-django-dskgis.git
```

2. Change the directory to the cloned repository:
```bash
cd deploy-django-dskgis
```

3. Add the following environment variables to the `.env` file:
   ( Create a .env file in the root directory of the project and add fill out the following environment variables )
   NOTE: Credentials are for testing purposes only. Do not use them in production.
   NOTE: Replace the `AWS_S3_ENDPOINT_URL` with the IP address of your machine 
```bash
ADMIN_USER_EMAIL='admin@example.com'
ADMIN_USER_PASSWD='admin123456'
AWS_ACCESS_KEY_ID='accesskey'
AWS_S3_ENDPOINT_URL='http://192.168.1.101:9000'
AWS_SECRET_ACCESS_KEY='secretkey'
AWS_STORAGE_BUCKET_NAME='django-dskgis'
CACHE_URL='redis://redis:6379/1'
CSRF_TRUSTED_ORIGINS='https://localhost,https://127.0.0.1,https://*.azat.host'
DATABASE_URL='psql://postgres:djazz@postgres:5432/postgres'
DEBUG='True'
POSTGRES_PASSWORD='djazz'
STAFF_USER_EMAIL='staff@example.com'
STAFF_USER_PASSWD='staff123456'
```


4. Run the following command to deploy the application:
```bash
docker compose up
```
OR 
```bash
docker-compose up -d
```
which will run the application in the background.

5. Open a new terminal window and run the following commands:

```bash
docker compose exec -it djazz python manage.py collectstatic --no-input
```
```bash
docker compose exec -it djazz python manage.py createsuperuser
```

## Endpoints and usage: 

This project follows OpenAPI standards, check for usage and endpoints at: http://127.0.0.1:8000

![CleanShot 2024-08-26 at 12.32.25](https://raw.githubusercontent.com/azataiot/images/master/2024/08/upgit_20240826_1724664748.png)

# FAQ

There is 404 or 403 error serving the static files. What should i do ? 

Is such case, it might be because of the following: 

1. Your machine already using port 9000 and port 9001 for something else. Stop that container and restart this.
2. Your minio bucket needs to be public, go to https://127.0.0.1:9000 and login with `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`, change the bucket Access policy to Public (as shown below in the picture)

![CleanShot 2024-08-26 at 12.30.54](https://raw.githubusercontent.com/azataiot/images/master/2024/08/upgit_20240826_1724664694.png)
