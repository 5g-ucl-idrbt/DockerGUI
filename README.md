# DockerGUI
Create DOcker with GUI





# Install VNC Server on Ubuntu

This project is Virtual Network Computing, or VNC, is a connection system that allows you to use your keyboard and mouse to interact with a graphical desktop environment on a remote server..

## Installation  TightVncServer on Ubuntu(Server)

Installing the Desktop Environment and vncserver 

```bash
  $sudo apt update
    Now install Xfce along with the xfce4-goodies package
  $sudo apt install xfce4 xfce4-goodies
  $sudo apt install tightvncserver
    vncserver command to set a VNC access password
  $vncserver
    Output
        You will require a password to access your desktops.

        Password:
        Verify:  
    
     It launches a default server instance on port 5901
    Output
Would you like to enter a view-only password (y/n)? n
xauth:  file /home/praveena/.Xauthority does not exist

New 'X' desktop is your_hostname:1

Creating default startup script /home/praveena/.vnc/xstartup
Starting applications specified in /home/praveena/.vnc/xstartup
Log file is /home/praveena/.vnc/your_hostname:1.log
    
  Reference link:https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-20-04
```

Configuring the VNC Server

```bash
     
   $vncserver -kill :1
   $mv ~/.vnc/xstartup ~/.vnc/xstartup.bak
   $nano ~/.vnc/xstartup
      add the following lines to the file
      #!/bin/bash
      xrdb $HOME/.Xresources
      startxfce4 &
    $chmod +x ~/.vnc/xstartup
    $vncserver -localhost

    Output
New 'X' desktop is your_hostname:1

Starting applications specified in /home/praveena/.vnc/xstartup
Log file is /home/praveena/.vnc/your_hostname:1.log
  

  
```
Runnng VNC as a System Service

```bash
  $sudo nano /etc/systemd/system/vncserver@.service
  [Unit]
Description=Start TightVNC server at startup
After=syslog.target network.target

[Service]
Type=forking
User=sammy
Group=sammy
WorkingDirectory=/home/sammy

PIDFile=/home/sammy/.vnc/%H:%i.pid
ExecStartPre=-/usr/bin/vncserver -kill :%i > /dev/null 2>&1
ExecStart=/usr/bin/vncserver -depth 24 -geometry 1280x800 -localhost :%i
ExecStop=/usr/bin/vncserver -kill :%i

[Install]
WantedBy=multi-user.target
  
  $sudo systemctl daemon-reload
  $sudo systemctl enable vncserver@1.service
  $vncserver -kill :1
  $sudo systemctl start vncserver@1
  $sudo systemctl status vncserver@1
```
## Installation  TightVNCViwer on Ubuntu(Client)
```bash
  $sudo apt update
  $sudo apt install tigervnc-viewer
  
  1) once Once the installation is complete, you can launch TigerVNC Viewer either from the command line by typing vncviewer or by searching for "TigerVNC Viewer" in your desktop environment's application launcher.

  2)When the TigerVNC Viewer opens, you can enter the IP address or hostname of the remote VNC server you want to connect to in the "VNC Server" field. Specify the display number if applicable (e.g., 192.168.138.121:1 or 192.168.138.121:5901).

  3)Click the "Connect" button to establish a connection to the remote VNC server.

  4)If the remote VNC server requires authentication, you will be prompted to enter the password you set during the VNC server setup.
```

## Installation  VNCServer(Docker image) on Ubuntu(Bare metal)
Installing Docker,Run VncServer docker image,connecting VncServer through vncviewer


```bash
  $sudo apt update
  $sudo apt install apt-transport-https ca-certificates curl software-properties-common
  $curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  $sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
  $apt-cache policy docker-ce
  $sudo apt install docker-ce
  $sudo systemctl status docker
  
  1) Forward VNC service port 5900 to host by
  docker run -p 6080:80 -p 5900:5900 -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc

  2)Now, open the vnc viewer and connect to port 5900. If you would like to protect vnc service by password, set environment variable VNC_PASSWORD, for example
  docker run -p 6080:80 -p 5900:5900 -e VNC_PASSWORD=mypassword -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc

  3)A prompt will ask password either in the browser or vnc viewer.

  4)Run below commands to to run the docker images,and connect the vnc server
  Showing the all docker images
  a)$sudo docker ps
  Run the vncserver image 
  b)$sudo docker exec -it interesting_mcclintock bash
  it will enter into the container
  then type ipconfig to identify the docker ip address
  ex:172.17.0.2
  c)open any vnc viewer(TightVNCViewer,RealVNCViewer..) add  docker ip address:vncserverport (172.17.0.2:5900) 
  d) vnc viewer ask for password(mypassword) then it will connect to vncserver
  e) we have to connect the vncserver from vncviewer(client) we need to add a route in vncviewer(pc)
  $sudo ip route add dockerip(172.17.02) via baremetalip(which is the vncserver is installed (192.168.138.123))

  Reference Link : 



# Install VNC Server on Ubuntu

This project is Virtual Network Computing, or VNC, is a connection system that allows you to use your keyboard and mouse to interact with a graphical desktop environment on a remote server..

## Installation  TightVncServer on Ubuntu(Server)

Installing the Desktop Environment and vncserver 

```bash
  $sudo apt update
    Now install Xfce along with the xfce4-goodies package
  $sudo apt install xfce4 xfce4-goodies
  $sudo apt install tightvncserver
    vncserver command to set a VNC access password
  $vncserver
    Output
        You will require a password to access your desktops.

        Password:
        Verify:  
    
     It launches a default server instance on port 5901
    Output
Would you like to enter a view-only password (y/n)? n
xauth:  file /home/praveena/.Xauthority does not exist

New 'X' desktop is your_hostname:1

Creating default startup script /home/praveena/.vnc/xstartup
Starting applications specified in /home/praveena/.vnc/xstartup
Log file is /home/praveena/.vnc/your_hostname:1.log
    
  Reference link:https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-20-04
```

Configuring the VNC Server

```bash
     
   $vncserver -kill :1
   $mv ~/.vnc/xstartup ~/.vnc/xstartup.bak
   $nano ~/.vnc/xstartup
      add the following lines to the file
      #!/bin/bash
      xrdb $HOME/.Xresources
      startxfce4 &
    $chmod +x ~/.vnc/xstartup
    $vncserver -localhost

    Output
New 'X' desktop is your_hostname:1

Starting applications specified in /home/praveena/.vnc/xstartup
Log file is /home/praveena/.vnc/your_hostname:1.log
  

  
```
Runnng VNC as a System Service

```bash
  $sudo nano /etc/systemd/system/vncserver@.service
  [Unit]
Description=Start TightVNC server at startup
After=syslog.target network.target

[Service]
Type=forking
User=sammy
Group=sammy
WorkingDirectory=/home/sammy

PIDFile=/home/sammy/.vnc/%H:%i.pid
ExecStartPre=-/usr/bin/vncserver -kill :%i > /dev/null 2>&1
ExecStart=/usr/bin/vncserver -depth 24 -geometry 1280x800 -localhost :%i
ExecStop=/usr/bin/vncserver -kill :%i

[Install]
WantedBy=multi-user.target
  
  $sudo systemctl daemon-reload
  $sudo systemctl enable vncserver@1.service
  $vncserver -kill :1
  $sudo systemctl start vncserver@1
  $sudo systemctl status vncserver@1
```
## Installation  TightVNCViwer on Ubuntu(Client)
```bash
  $sudo apt update
  $sudo apt install tigervnc-viewer
  
  1) once Once the installation is complete, you can launch TigerVNC Viewer either from the command line by typing vncviewer or by searching for "TigerVNC Viewer" in your desktop environment's application launcher.

  2)When the TigerVNC Viewer opens, you can enter the IP address or hostname of the remote VNC server you want to connect to in the "VNC Server" field. Specify the display number if applicable (e.g., 192.168.138.121:1 or 192.168.138.121:5901).

  3)Click the "Connect" button to establish a connection to the remote VNC server.

  4)If the remote VNC server requires authentication, you will be prompted to enter the password you set during the VNC server setup.
```

## Installation  VNCServer(Docker image) on Ubuntu(Bare metal)
Installing Docker,Run VncServer docker image,connecting VncServer through vncviewer


```bash
  $sudo apt update
  $sudo apt install apt-transport-https ca-certificates curl software-properties-common
  $curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  $sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
  $apt-cache policy docker-ce
  $sudo apt install docker-ce
  $sudo systemctl status docker
  
  1) Forward VNC service port 5900 to host by
  docker run -p 6080:80 -p 5900:5900 -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc

  2)Now, open the vnc viewer and connect to port 5900. If you would like to protect vnc service by password, set environment variable VNC_PASSWORD, for example
  docker run -p 6080:80 -p 5900:5900 -e VNC_PASSWORD=mypassword -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc

  3)A prompt will ask password either in the browser or vnc viewer.

  4)Run below commands to to run the docker images,and connect the vnc server
  Showing the all docker images
  a)$sudo docker ps
  Run the vncserver image 
  b)$sudo docker exec -it interesting_mcclintock bash
  it will enter into the container
  then type ipconfig to identify the docker ip address
  ex:172.17.0.2
  c)open any vnc viewer(TightVNCViewer,RealVNCViewer..) add  docker ip address:vncserverport (172.17.0.2:5900) 
  d) vnc viewer ask for password(mypassword) then it will connect to vncserver
  e) we have to connect the vncserver from vncviewer(client) we need to add a route in vncviewer(pc)
  $sudo ip route add dockerip(172.17.02) via baremetalip(which is the vncserver is installed (192.168.138.123))

  Reference Link:



# Install VNC Server on Ubuntu

This project is Virtual Network Computing, or VNC, is a connection system that allows you to use your keyboard and mouse to interact with a graphical desktop environment on a remote server..

## Installation  TightVncServer on Ubuntu(Server)

Installing the Desktop Environment and vncserver 

```bash
  $sudo apt update
    Now install Xfce along with the xfce4-goodies package
  $sudo apt install xfce4 xfce4-goodies
  $sudo apt install tightvncserver
    vncserver command to set a VNC access password
  $vncserver
    Output
        You will require a password to access your desktops.

        Password:
        Verify:  
    
     It launches a default server instance on port 5901
    Output
Would you like to enter a view-only password (y/n)? n
xauth:  file /home/praveena/.Xauthority does not exist

New 'X' desktop is your_hostname:1

Creating default startup script /home/praveena/.vnc/xstartup
Starting applications specified in /home/praveena/.vnc/xstartup
Log file is /home/praveena/.vnc/your_hostname:1.log
    
  Reference link:https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-20-04
```

Configuring the VNC Server

```bash
     
   $vncserver -kill :1
   $mv ~/.vnc/xstartup ~/.vnc/xstartup.bak
   $nano ~/.vnc/xstartup
      add the following lines to the file
      #!/bin/bash
      xrdb $HOME/.Xresources
      startxfce4 &
    $chmod +x ~/.vnc/xstartup
    $vncserver -localhost

    Output
New 'X' desktop is your_hostname:1

Starting applications specified in /home/praveena/.vnc/xstartup
Log file is /home/praveena/.vnc/your_hostname:1.log
  

  
```
Runnng VNC as a System Service

```bash
  $sudo nano /etc/systemd/system/vncserver@.service
  [Unit]
Description=Start TightVNC server at startup
After=syslog.target network.target

[Service]
Type=forking
User=sammy
Group=sammy
WorkingDirectory=/home/sammy

PIDFile=/home/sammy/.vnc/%H:%i.pid
ExecStartPre=-/usr/bin/vncserver -kill :%i > /dev/null 2>&1
ExecStart=/usr/bin/vncserver -depth 24 -geometry 1280x800 -localhost :%i
ExecStop=/usr/bin/vncserver -kill :%i
/home/idrbt/api.video-android-live-stream
[Install]
WantedBy=multi-user.target
  
  $sudo systemctl daemon-reload
  $sudo systemctl enable vncserver@1.service
  $vncserver -kill :1
  $sudo systemctl start vncserver@1
  $sudo systemctl status vncserver@1
```
## Installation  TightVNCViwer on Ubuntu(Client)
```bash
  $sudo apt update
  $sudo apt install tigervnc-viewer
  
  1) once Once the installation is complete, you can launch TigerVNC Viewer either from the command line by typing vncviewer or by searching for "TigerVNC Viewer" in your desktop environment's application launcher.

  2)When the TigerVNC Viewer opens, you can enter the IP address or hostname of the remote VNC server you want to connect to in the "VNC Server" field. Specify the display number if applicable (e.g., 192.168.138.121:1 or 192.168.138.121:5901).

  3)Click the "Connect" button to establish a connection to the remote VNC server.

  4)If the remote VNC server requires authentication, you will be prompted to enter the password you set during the VNC server setup.
```

## Installation  VNCServer(Docker image) on Ubuntu(Bare metal)
Installing Docker,Run VncServer docker image,connecting VncServer through vncviewer


```bash
  $sudo apt update
  $sudo apt install apt-transport-https ca-certificates curl software-properties-common
  $curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  $sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
  $apt-cache policy docker-ce
  $sudo apt install docker-ce
  $sudo systemctl status docker
  
  1) Forward VNC service port 5900 to host by
  docker run -p 6080:80 -p 5900:5900 -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc

  2)Now, open the vnc viewer and connect to port 5900. If you would like to protect vnc service by password, set environment variable VNC_PASSWORD, for example
  docker run -p 6080:80 -p 5900:5900 -e VNC_PASSWORD=mypassword -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc

  3)A prompt will ask password either in the browser or vnc viewer.

  4)Run below commands to to run the docker images,and connect the vnc server
  Showing the all docker images
  a)$sudo docker ps
  Run the vncserver image 
  b)$sudo docker exec -it interesting_mcclintock bash
  it will enter into the container
  then type ipconfig to identify the docker ip address
  ex:172.17.0.2
  c)open any vnc viewer(TightVNCViewer,RealVNCViewer..) add  docker ip address:vncserverport (172.17.0.2:5900) 
  d) vnc viewer ask for password(mypassword) then it will connect to vncserver
  e) we have to connect the vncserver from vncviewer(client) we need to add a route in vncviewer(pc)
  $sudo ip route add dockerip(172.17.02) via baremetalip(which is the vncserver is installed (192.168.138.123))
  Reference Link:https://hub.docker.com/r/dorowu/ubuntu-desktop-lxde-vnc#quick-start


```














    


```














    


```














    
