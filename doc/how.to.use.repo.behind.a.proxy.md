how to use repo behind a proxy
===

install socat
---
```
#apt-get install socat
```
create gitproxy
---
```
#!/bin/sh
# Use socat to proxy git through an HTTP CONNECT firewall.
# Useful if you are trying to clone git:// from inside a company.
# Requires that the proxy allows CONNECT to port 9418.
#
# Save this file as gitproxy somewhere in your path (e.g., ~/bin) and then run
# chmod +x gitproxy
# git config --global core.gitproxy gitproxy
#
# More details at http://tinyurl.com/8xvpny

# Configuration. Common proxy ports are 3128, 8123, 8000.
#_proxy=172.16.2.17
_proxy=10.10.40.10
_proxyport=80

myname=YourName
mypassword=YourPassword

exec socat STDIO
PROXY:$_proxy:$1:$2,proxyport=$_proxyport,proxyauth=$myname:$mypassword
```
replace with your **YourName** and **YourPassword**. 
add gitproxy to your path and config gitproxy
---
```
#git config --global core.gitproxy gitproxy
```
