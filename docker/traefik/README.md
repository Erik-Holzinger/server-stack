# Traefik

## <a name="attention"></a>Attention
This Traefik configuration is using netcup as a provider for the DNS challenge.
For different [providers](https://doc.traefik.io/traefik/https/acme/#providers) or different types of [challenges](https://doc.traefik.io/traefik/user-guides/docker-compose/acme-tls/) please refer to the official documentation.
If required, changes must be made in the `./config/traefik.yml` and the `docker-compose.yml` file.

## Configuration

### 1. Adjust traefik's static configuration
Please specify the correct E-Mail for the certificate registration inside the `./config/traefik.yml` file.
Depending on your provider and challenge type, multiple changes are required, see [Attention](#attention).

### 2. Adjust environment variables
Copy and rename the `example.env` to `.env` and adjust the variables inside this file.

### 3. Change password for dashboard authentication
Change the password for the admin user of the traefik dashboard in the `./config/dynamic.yml` file.
As the [traefik documentation](https://doc.traefik.io/traefik/middlewares/http/basicauth/) describes, htpasswd must be used to create the password string.
IMO the easiest way to do it is using [htpasswd docker container](https://github.com/xmartlabs/docker-htpasswd).

### 4. (Optional) Add external services
External services can be added in the `./config/dynamic.yml` file as seen in the example below:
```
http:
  routers:
    test-service:
      rule: "Host(`foo.bar.example`)"
      service: test-service
      entryPoints:
        - websecure
  services:
    test-service:
      loadBalancer:
        servers:
          - url: "http://192.168.10.10:8080"
```
