


# Installation  VNCServer(Docker image) on Ubuntu(Bare metal)




Run VncServer docker image,connecting VncServer through vncviewer



  ### Create docker Image from dockerhub
  1)pull the vnc server docker image

  `sudo docker pull dorowu/ubuntu-desktop-lxde-vnc`
  
  2)Run the docker image
  
  `sudo docker run -p 6080:80 -p 5900:5900 -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc`
 
  3)Set VNC_PASSWORD

  `sudo docker run -p 6080:80 -p 5900:5900 -e VNC_PASSWORD=mypassword -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc`

  4)Docker Exec a command
  
  `sudo docker exec -it interesting_mcclintock bash`
      
## Installation  TightVNCViwer on Ubuntu(Client)

  `sudo apt update`

  `sudo apt install tigervnc-viewer`
  
