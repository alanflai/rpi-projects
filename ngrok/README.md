# rpi-projects
## ngrok

For our Raspberry Pi project  which needs to expose a service on the public Internet (ex HTTP/HTTPS service), through DSL domestic connection behind NAT, we use
**ngrok** [Web site] (http://www.ngrok.com) public tunneling service. For our purpose (development and demostration) the free options of the service is enough.

In our development environment the Raspberry Pi computer uses WiFi connection to link the domestic Wifi Lan, wich ha natted IPs. The public Internet connection
is made through the DSL conection wich has a public IP, NATTED towards the internal LAN IPs.

To use **ngrok**  we need to follow these steps:

1. First register online to ngrock's web site. After that we receive an authentication token (Auth Token) to use in the next steps
2. Download the ngrock client software. In our case AMD 64 distribution for Raspberry Pi 4 (a tgz file)
3. Unzip the downloaded software into /usr/bin. In this way the ngrok executable is  
   into user's path and can be executed from every system folders. Change the ngrock's ownership to root:root
4. At this point activate the configuration using the received [Auth Token], from the command line execute the following command
	'> ngrok authtoken [Auth Token]' 
   This command creates the hidden directory .ngrok2 into the home directory of the current user. Inside this directory is created the
   ngrok.yml, ngrok's configuration file in which is saved the [Auth Toke] and could be inserted in a secnd moment other configurations
5. Copy the shell scripts start-ngrok.sh and stop-ngork.sh into "/usr/bin2" folder, change their ownership to root:root 
   and change  execution permissions to 755
6. To start a new ngrok tunnel give this command from a terminal
   '> . start-ngrok.sh [TCP port number]'
   if no port is assigned the script use the defaukt oort (8080)
   The script displays in stdout the public tunnel's URL and save this value into the environment variable NGROK_PUBLIC_URL
7. To watch the status of the established ngrok's tunnel, open the browser to the following url: http://localhost:4040
8. To stop the tunnel, instead, give this command from a terminal
   '> . stop-ngrok.sh'

The two aforementioned  scripts, archived in this git repository, are been inspired by the blog discussions [How to run ngrok in background?]
(https://stackoverflow.com/questions/27162552/how-to-run-ngrok-in-background).
