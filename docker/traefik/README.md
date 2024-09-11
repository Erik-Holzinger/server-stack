# Traefik

## <a name="attention"></a>Attention
This Traefik configuration is using netcup as a provider for the DNS challenge.
For different [providers](https://doc.traefik.io/traefik/https/acme/#providers) or different types of [challenges](https://doc.traefik.io/traefik/user-guides/docker-compose/acme-tls/) please refer to the official documentation.
If required, changes must be made in the `config/traefik.yml` and the `docker-compose.yml` file.

## Configuration

### 1. Adjust traefik's static configuration
Please specify the correct E-Mail for the certificate registration inside the `config/traefik.yml` file.
Depending on your provider and challenge type, multiple changes are required, see [Attention](#attention).

### 2. Change password for dashboard authentication
Change the password for the admin user of the traefik dashboard in the `config/dynamic.yml` file.
As the [traefik documentation](https://doc.traefik.io/traefik/middlewares/http/basicauth/) describes, htpasswd must be used to create the password string.
IMO the easiest way to do it is using [htpasswd docker container](https://github.com/xmartlabs/docker-htpasswd).

### 3. Adjust environment variables
Copy and rename the `example.env` to `.env` and adjust the variables inside this file.

### 4. Create folder and files
Create the folder configured in the `.env` file for traefik's logs using `mkdir logs`.
Create the `acme.json` file using `touch config/acme.json` and adjust the permission using `chmod 600 config/acme.json` 

### 5. Adjust router rules
Replace the router rules for the traefik dashboard and the whoami service in the `docker-compose.yml` file.

### 6. (Optional) Switch to production certificates
Comment the line for disabling the staging CA in the

### 7. (Optional) Add external services
External services can be added in the `config/dynamic.yml` file as seen in the example below:
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
