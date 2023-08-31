# Virtual Proxy Server
This is a guide for creating your own proxy server using VirtualBox. I am using the following software versions:
- VirtualBox 7.0.10 (macOS)
- Ubuntu 22.04.3 LTS



# Squid Proxy Server
All of the commands assume that you are using root priviledges. If you aren't, just add sudo to the start of each command used.

Update your Ubuntu repositories before starting with:
```
apt-get update
```
Once you're updated, install Squid with the command:
```
apt-get install squid
```
Initial configuration changes will be made in the squid.conf file.
```
nano /etc/squid/squid.conf
```
By default, Squid uses port 3218. If you wish to use another port for your proxy, you can change the http_port setting with the port you wish to use. There are multiple modes you can use, including IP-Layer NAT interception that delivers traffic to the Squid port. You will have to set a second port with this argument.
```
http_port 3218
http_port 8080 intercept
```
Another default of Squid is the denial of all http traffic. You can change this to all all by changing the http_access setting.
```
http_access allow all
```
After the changes to these configurations are complete, you will need to restart squid.
```
systemctl restart squid
```
To ensure that Squid comes back up on start in the event that the VM is ever shut down, you can enable it with the following command:
```
systemctl enable squid
```

Once these steps are done, you can go to your network settings on your client workstation and enable the proxy using your new proxy server IP and port.

There are more configurations you can make to Squid, such as:
- Creating an Access Control List
- Configuring Authentication
- Adding Users/Passwords
- Blocking Websites
