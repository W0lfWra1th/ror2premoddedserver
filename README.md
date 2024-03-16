# Risk of Rain 2 Premodded Server

# Table of Contents
1. Explanation and Purpose
2. quickstart
3. configuration
4. modding
5. Questions and Answers
6. Acknowledgements

# 1. Purpose and Explanation

This is a Docker image that can setup a docker container for a Risk of Rain 2 dedicated server 
on a linux machine that already has the necessary mods in order for it to be changed to ver 1.2.4.4,
which is required since the default server version is out of date for it to be used by the game. I created this 
for a few reasons, mainly for myself becuase I had various issues doing this and I wanted a simple 
and reliable way of setting this up. However, I also saw various users on platforms like Reddit that 
were having issues creating their own dedicated servers or modding their own already created servers. 
Hopefully, this will help them (and me) in their adventure to play with 15 of their friends with mods 
while using the friendly fire artifact...

# 2. Quickstart

 [Docker](https://docs.docker.com/get-docker/) is required for this to work. 
You will need to find out how to install it on your linux distribution on your own.

The container can be started with:
```bash
docker run -d --rm -p 27015:27015/udp w0lfwra1th/ror2premoddedserver:latest
```
To connect to the server, start the game and press CTRL+ALT+` which will then open the developer console

Then enter either the public ip address of the server or, if it is on the same network as you, the internal ip address of your server into this command below: 
```
connect "<server ip>:27015";
```
Example: connect "111.111.11.111:27015";

# 3. configuration

In order to configure the server to do things like change the player count, add a password, or 
change the port that it uses, you need to use enviroment variables when creating the container. These can be 
specified by using -e and then the enviroment variable with the option you want.

An example of this is:
```
docker run -d --rm -p 27015:27015/udp -e R2_PSW='1234' w0lfwra1th/ror2premoddedserver:latest
```
This makes it so that you will need the password "1234" to join the server.

The command to join a server set up this way would be:
```
cl_password "1234"; connect "<server ip>:27015";
```
Below are all of the enviroment variables:

R2_PLAYERS = sets number of players allowed. Max is 16, default is 4

R2_HEARTBEAT = advertizes to the steam (not ingame) server browser (currently not working)

R2_HOSTNAME = The name that would appear in the steam server browser.

R2_PSW = Adds a password to be able to connect to the server, specified as R2_PSW='<password>'

R2_CUSTOM_MODS = If you decide to install your own mods, use this option by setting it like: R2_CUSTOM_MODS=1 

WARNING: If enabled, This option will actually remove the included BepInEx folder which is currently necessary to be able to load the server. If you 
do this, you will need to include the version swapper mod and all of its dependencies into your own custom BepInEx folder which will be explained in the modding section of these instructions.

R2_QUERY_PORT = used to specify the port to steamworks so that the server can be listed in the steam server browser (currently not working)

R2_SV_PORT = changes the port that is used for the game server. EX: R2_SV_PORT=00000

R2_GAMEMODE = changes gamemode to either ClassicRun (default) or InfiniteTowerRun (simulacrum) EX: R2_GAMEMODE=InfiniteTowerRun

R2_TAGS = Adds tags that will be shown in the server browser EX: R2_TAGS='tag'

# 4. Modding

First, you will need to download these files from [thunderstore.io](https://thunderstore.io/package/)

1. [BepInExPack](https://thunderstore.io/package/bbepis/BepInExPack/)
2. [R2API](https://thunderstore.io/package/tristanmcpherson/R2API/)
3. [HookGenPatcher](https://thunderstore.io/package/RiskofThunder/HookGenPatcher/)
4. [VersionChangerServer](https://thunderstore.io/package/theniklev/VersionChangerServer/)

work in progress :)












