### How to run

#### Environment Variables

docker compose will use .env in the same directory as the yaml

```
VPN_USER=
VPN_PASS=
```

Run with
```
sudo docker compose up -d
```
### Debugging

container specific logs accessible at
```
/var/lib/docker/containers/<container id>/<container-json.log>
```

### Files management

- default save directory in docker: `/config/qBittorrent/downloads`
___
From https://hub.docker.com/r/binhex/arch-qbittorrentvpn/

### User Permissions

>User ID (PUID) and Group ID (PGID) can be found by issuing the following command for the user you want to run the container as:-

> `id <username>`

I recommend setting puid and pgid to your desired user. Using 0 as root will run into permissions issues.

### OpenVPN (pre-requisite)

> Please note this Docker image does not include the required OpenVPN configuration file and certificates. These will typically be downloaded from your VPN providers website (look for OpenVPN configuration files), and generally are zipped.

>PIA users - The URL to download the OpenVPN configuration files and certs is: https://www.privateinternetaccess.com/openvpn/openvpn.zip

>Once you have downloaded the zip (normally a zip as they contain multiple ovpn files) then extract it to `/<bound host volume location>/docker/config/openvpn/` folder (if that folder doesn't exist then start and stop the docker container to force the creation of the folder).

>If there are multiple ovpn files then please delete the ones you don't want to use (normally filename follows location of the endpoint) leaving just a single ovpn file and the certificates referenced in the ovpn file (certificates will normally have a crt and/or pem extension).

### Access qBittorrent (web ui)

http://localhost:8080/
>Username:- admin  
Password:- randomly generated, password shown in `/<bound host volume location>/docker/config/supervisord.log`

in the logs should be the line containing this text:  
`The WebUI administrator password was not set. A temporary password is provided for this session`

After logging into webui at localhost:8080 you can change the password to whatever you like

You can confirm that your VPN is working by checking qBittorrent logs for external IP

### Access Privoxy

http://localhost:8118

### Access microsocks

http://localhost:9118
>default credentials: admin/socks