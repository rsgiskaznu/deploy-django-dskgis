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

5. Open a new terminal window and run the following command to create a superuser:
```bash
docker exec -it django-dskgis_web_1 python manage.py createsuperuser
```

# API Endpoints

- `/api/v1/` - The root endpoint
