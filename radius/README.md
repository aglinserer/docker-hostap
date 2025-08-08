# Information primarily on https://hub.docker.com/r/freeradius/freeradius-server/

# Docker Build
Only the relevant excerpts for me are here:
```
docker build -t my-radius-image -f Dockerfile .
docker run --rm -d --name my-radius -p 1812-1813:1812-1813/udp my-radius-image
```
And to test
```
radtest bob test 127.0.0.1 0 testing123
```

# Configuration

Create a local Dockerfile based on the required image and COPY in the server configuration.

```
FROM freeradius/freeradius-server:latest
COPY raddb/ /etc/raddb/
```
The raddb directory could contain, for example:

```
clients.conf
mods-config/
mods-config/files/
mods-config/files/authorize
```
Where clients.conf contains a simple client definition
```
client dockernet {
	ipaddr = 172.17.0.0/16
	secret = testing123
}
```
and the authorize "users" file contains a test user:

```
bob	Cleartext-Password := "test"
```
