docker-openwrt-ftp
===================

An image based on OpenWrt x86_64 which runs a ftp server.

How to use
----------

The simplest case is to specify user name and password when starting
the container:

```bash
docker run -p 11021:21 -it --rm -e FTP_USER=root -e FTP_PASS=toor -e HOST=127.0.0.1 mcreations/ftp
```

Note that ```HOST``` signifies the name or IP with which the docker
container can be reached from clients, usually the public IP or
name of the docker host where the container is started.

Now, you can ftp to this docker instance with

```bash
ftp 127.0.0.1 11021
```

#### Passive ports

The default configuration uses passive ports from 65000 to 65100. If
you need to publish a specific port range on your host, you can narrow
down the range with the environment variables `PASV_MIN_PORT` and `PASV_MAX_PORT`.

```bash
docker run -it --rm \
            -p 11021:21 \
            -e FTP_USER=root -e FTP_PASS=toor -e HOST=127.0.0.1 \
            -p 65000-65004:65000-65004 \
            -e PASV_MIN_PORT=65000 -e PASV_MAX_PORT=65004 \
            mcreations/ftp


