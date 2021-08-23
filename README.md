# TeamCity-Server

Dockerized TeamCity with SSL support using NGINX and Let's Encrypt

---

# Requirements

Docker and docker-compose:

* https://docs.docker.com/engine/installation/
* https://docs.docker.com/compose/install/

---

# Usage

### 1. Set up a VM with a URL pointing at it.

```shell
e.g. yoururlhere.com
```

### 2. Set up the environment variables

Add the following variables to the env file.

```shell
# DNS
VIRTUAL_HOST_LIST=yoururlhere.com

# HTTPS
HTTPS_ENABLED=true
LETSENCRYPT_HOST_LIST=yoururlhere.com
LETSENCRYPT_EMAIL=you@yoururlhere.com

# TEAMCITY
TEAMCITY_DIR=/volumes/teamcity
```

### 3. Copy the docker-compose file to the root dir

### 4. Set permissions for the Team City volume path

```shell
chmod -R 777 /volumes/teamcity
```

### 5. Bring up the services

```
docker-compose up -d
```

### 6. Initial Superuser authentication

Access the Team City UI at the given URL above (yoururlhere.com)

```shell
tail -f /volumes/teamcity/logs/teamcity-server.log
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
