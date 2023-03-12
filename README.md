# owncloud-nginx-letsencrypt-docker

This is a simple repo with information on the a `docker-compose.yml` to run [ownCloud](https://owncloud.org/) with an Nginx proxy and LetsEncrypt using Docker.

## Information sources

This is consolidated based on information from the following places and thanks to them:
- [ownCloud documentation](https://doc.owncloud.com/server/next/admin_manual/installation/docker/#docker-compose)
- [previous implementation](https://github.com/rorydavidson/owncloud-nginx-letsencrypt-docker)

## Get started

Set up the necessary environment variables at the command line (or equivalent method on the relevant operating system):

```bash
cat << EOF >| .env
LETSENCRYPT_EMAIL=info@your.domain.com
OWNCLOUD_VERSION=10.11
OWNCLOUD_DOMAIN=your.domain.com:8080
OWNCLOUD_TRUSTED_DOMAINS=your.domain.com
ADMIN_USERNAME=admin
ADMIN_PASSWORD=admin
HTTP_PORT=8080
EOF
```

The webserver is nginx-proxy and it will listen on ports 80 and 443 by default, redirecting traffic to HTTPS for your ownCloud instance. Make sure to have both port open on the firewall. The HTTP_PORT environment variable sets which port ownCloud itself will listen internally.

Then run

```bash
docker-compose up -d
```

You should then be able to access it at the domain name you entered and it will redirect to the https URL with a valid certificate.
