# reverse-proxy
Setups virtual host reverse proxies on a Linux machine so that *your-app.your-domain.com* links whatever local port you gave. Once installed, non-root users will be able to add or update virtual hosts reverse proxies.

## Basic Usage

### Installation

 1. From a Debian machine (e.g., Ubuntu)
 2. Install Nginx: `$ sudo apt-get install nginx`
 3. `$ sudo reverse-proxy install`

You can *uninstall* later via `$ sudo reverse-proxy uninstall`.

### Setting up or updating a reverse proxy

    $ reverse-proxy add my-app.my-domain.com 127.0.0.1:8080
    
Supposing that `my-app.my-domain.com` points to your machine's IP, now going opening `http://my-app.my-domain.com` in your browser will try to connect to `127.0.0.1:8080` on your machine.

### Using with Docker

This is really useful for **[Docker](http://www.docker.com/)** (with or without [docker-compose](http://blog.docker.com/tag/docker-compose/), previously [Fig](http://fig.sh)).

Supposing you've a `docker-compose.yml` that looks somewhat like (not this will use a *random* port):

    web:
      build: .
      ports:
       - 127.0.0.1:*:80

Now you can make your server serve it via:

    $ docker-compose up -d
    $ reverse-proxy add myapp.example.com $(docker-compose port web 80)
