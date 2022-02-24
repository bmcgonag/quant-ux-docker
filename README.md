# Quant-UX for Docker

Quant-UX is a great open source prototyping / mock-up application created by [Klaus Schaefers](https://github.com/KlausSchaefers).

I started working to make this into a dockerized application as a way to help encourage the continued development of the tool. 

The DockerFiles use the smallest images I could find as a base, and the docker-compose is really setup to allow for the easiest deployment possible. 

## Docker-Compose Details
To use the docker-compose.yml file, you can download just the compose file with the command:

`wget https://raw.githubusercontent.com/bmcgonag/quant-ux-docker/main/docker-compose.yml`

Or, you can clone the repository with the command 

`git clone https://github.com/bmcgonag/quant-ux-docker.git`

### Docker-Compose Environment Variables
You'll want to make a few modifications to some of the environment variables.

| ENV   | Example  | About  |
|---|---|---|
| QUX_PROXY_URL  | http://quant-ux-backend:8080  | This value should not be changed unless you change the container name for the back end, or the QUX_HTTP_PORT environment variable.  |
| QUX_HTTP_HOST  | http://quant-ux-frontend:8082  | This value should not be changed unless you change the container name for the front end. DO NOT Change the port number as it is where the container port is set.   |
| QUX_HTTP_PORT  | 8080  | The port where the backend service runs  |
| QUX_MONGO_DB  | quantux  | The name of the mongo database to be used by the application  |
| QUX_MONGO_TABLE  | quantux  | The name of the mongo table prefix to be used by the application  |
| QUX_MAIL_USER  | admin@example.com  | The username for your smtp server  |
| QUX_MAiL_PASSWORD  | pa%%W0rD!  | The password for your smtp server user  |
| QUX_MAIL_HOST  | mail.example.com or smtp.example.com  | The host url of your smtp server  |
| QUX_JWT_PASSWORD | some-long-string-of-mix-case-chars-and-nums  | This is a java web token secret, and should be a very long password. You can use the generator at https://jwt.io/ and select RS256 for a very strong token. Never share this token with anyone.  |
| QUX_IMAGE_FOLDER_USER  | /qux-images  | A folder path for image storage in the container.  |
| QUX_IMAGE_FOLDER_APP  | /qux-image-app  | A folder path for image app storage in the container |
| TZ  | America/Chicago, Europe/London  | Your local timezone value. You can find your's with this list https://www.php.net/manual/en/timezones.php  |

### Docker Compose Por Mappings

| Port Host   | Port Container  |  Port Use  |
|---|---|---|
| 8082  | 8082  | This port is the port you'll use to access the application once it's up and running |

### Docker Compose Volume Mapping

| Host Folder   | Container Folder  | Volume Use  |
|---|---|---|
| ./data  | /data/db  | This volume is where the mongodb data is stored. It's wise to backup this folder to another system, or external storage in case of catastrophic events. |

