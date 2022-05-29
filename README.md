# Team City Server

Dockerised TeamCity with SSL

---

# Server Requirements

* Debian-based VM
* URL pointing at the VM
* Docker with Compose plugin: https://docs.docker.com/engine/install/ubuntu/
* Git: `apt install git`

---

# Usage

### 1. Clone this repo to the root of the server

```shell
git clone https://github.com/edjchapman/TeamCity-Server.git
cd TeamCity-Server
```

### 2. Set up the environment variables

```shell
# Update variables
cp .env.example .env
```

### 3. Set the URL of the TC Server in the buildAgent.properties files

### 4. Set permissions for the Team City volume path

```shell
mkdir -p /volumes/teamcity
chmod -R 777 /volumes/teamcity
```

### 5. Bring up the services

```
docker-compose up -d
```

### 6. Connecting to the database

- Use the credentials defined in the .env file.
- The host is the container_name:port (e.g. root_db_1:5432)

### 7. Initial Superuser authentication

Access the Team City UI at the given URL above (yoururlhere.com)

```shell
tail -f /volumes/teamcity/logs/logs/teamcity-server.log
```

Look out for output like this, the token is the one to use for initial authentication.

```shell
teamcity-server_1                    | =======================================================================
teamcity-server_1                    | TeamCity initialized, server UUID: 50c4d974-3b0e-95e0-b893-f63550f0bc41, URL: yoururlhere.com
teamcity-server_1                    | TeamCity is running in professional mode
teamcity-server_1                    | [TeamCity] Super user authentication token: 8768625104810134496 (use empty username with the token as the password to access the server)
```

---

# Troubleshooting

If the authentication token does not get generated, or there are other problems with the initial set up, it may be that
the server needs more resources.

---

# References

* https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion
* https://github.com/jwilder/nginx-proxy
* https://github.com/dataminelab/docker-jenkins-nginx-letsencrypt
* https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion/issues/277
* https://confluence.jetbrains.com/pages/viewpage.action?pageId=74845225#HowTo...-NGINX
* https://hub.docker.com/r/jetbrains/teamcity-server/
* https://confluence.jetbrains.com/display/TCD10/Using+HTTPS+to+access+TeamCity+server
