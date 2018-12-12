# Plex Nginx Reverse Proxy
 
This configuration will allow you to serve Plex via Nginx with **Remote Access support**. 
 
## Minimal Requirements
 
### Nginx:
* Module `ngx_stream_ssl_preread_module` compiled and loaded.
 
### Plex:
* Remote Access - enable
* Network - Custom server access URLs = `https://<your-domain>:443,http://<your-domain>:80`
* Network - Secure connections = Preferred. _Note you can force SSL by setting required and not adding the HTTP URL, however some players which do not support HTTPS (e.g: Roku, Playstations, some SmartTVs) will no longer function._
 
## Comments
 
* No need to deny port 32400 externally (Plex still pings over 32400, some clients may use 32400 by mistake despite 443 and 80 being set). Connection will still be encrypted when using `<your-domain>:32400`.
* Note adding `allowLocalhostOnly="1"` to your Preferences.xml, will make Plex only listen on the localhost, achieving the same thing as using a firewall. Set this only when deploying Nginx on the same host as Plex.
* When Remote Access check if performed, the connection is passed to Plex directly based on TLS SNI `*.plex.direct` domain.
* If you see `dnsmasq[...]: possible DNS-rebind attack detected`, please consider disabling [DNS Rebinding](https://support.plex.tv/articles/206225077-how-to-use-secure-server-connections/).

