# DockerGUI
Create DOcker with GUI






# Installation  VNCServer(Docker image) on Ubuntu(Bare metal)




Installing Docker,Run VncServer docker image,connecting VncServer through vncviewer


```bash
  $sudo apt update
  $sudo apt install apt-transport-https ca-certificates curl software-properties-common
  $curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  $sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
  $apt-cache policy docker-ce
  $sudo apt install docker-ce
  $sudo systemctl status docker
  1)pull the vnc server docker image
  $docker pull dorowu/ubuntu-desktop-lxde-vnc
  
  1) Forward VNC service port 5900 to host by
  $docker run -p 6080:80 -p 5900:5900 -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc

  2)docker run -p 6080:80 -p 5900:5900 -e VNC_PASSWORD=mypassword -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc
  3)A prompt will ask password either in the browser or vnc viewer.
 a)$sudo docker ps
 b)$sudo docker exec -it interesting_mcclintock bash
  
  then type ipconfig to identify the docker ip address
  ex:172.17.0.2
  c)open any vnc viewer(TightVNCViewer,RealVNCViewer..) add  docker ip address:vncserverport (172.17.0.2:5900) 
  d) vnc viewer ask for password(mypassword) then it will connect to vncserver
  e) we have to connect the vncserver from vncviewer(client) we need to add a route in vncviewer(pc)
  $sudo ip route add dockerip(172.17.02) via baremetalip(which is the vncserver is installed (192.168.138.123))
```
  
## Installation  TightVNCViwer on Ubuntu(Client)
```bash
  $sudo apt update
  $sudo apt install tigervnc-viewer
  ```




















    


```














    

















    















    


```














    
















    
