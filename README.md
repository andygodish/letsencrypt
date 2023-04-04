# Certbot 

## Prerequisites

docker, git

Automated way to generate certs via docker container.

```
git clone https://github.com/andygodish/certbot.git
```

Navigate to the new repo and follow the steps below.

### Domain Validation

Prove that you own the domain.

### Start webserver

```
docker run -it --rm --name nginx -v ${PWD}/nginx.conf:/etc/nginx/nginx.conf -v ${PWD}:/letsencrypt -v ${PWD}/certs:/etc/letsencrypt -p 80:80 -p 443:443 -d nginx
```

### Certbot

```
docker build . -t certbot

docker run -it --rm --name certbot -v ${PWD}:/letsencrypt -v ${PWD}/certs:/etc/letsencrypt certbot bash
```

/letsencrypt - challenges for lets encrypt (certbot will do this automatically for us)

/certs - back this up, folder used to store data and certificates generated by LE. 

### Issue a Certificate

`sudo certbot certonly --manual --preferred-challenges dns -d "*.DOMAIN"`

Add a new TXT record with your domain provider based on the output given by certbot command.

Verify with `nslookup -type=TXT _acme-challenge.DOMAIN` before continuing.

You want `fullchain.pem` and `privkey.pem` out of /live/DOMAIN/


