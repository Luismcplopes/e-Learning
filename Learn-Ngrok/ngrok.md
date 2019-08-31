# Ngrok
 - http://ngrok.com
 - https://ngrok.com/docs
 ## Install 
 ```bash
 wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-arm.zip
 sudo apt-get install unzip
 unzip /path/to/ngrok-stable-linux-arm.zip -d <destination_folder>
 ./ngrok authtoken 3pxvJXHKvyfff6BFN

```
 ## Run 
 ```bash
 ./ngrok http 80
 ./ngrok http -bind-tls=false -auth="username:password" 8080 #

#Rewrite the Host header to 'site.dev'
./ngrok http -host-header=rewrite site.dev:80
#Rewrite the Host header to 'example.com'
./ngrok http -host-header=example.com 80

 -subdomain=inconshreveable
  ```