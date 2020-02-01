# install-docker-ubuntu

faire un update des packages ubuntu   
```sudo apt-get update```   
installer les packages htop git 
```sudo apt-get -y install htop git iftop iotop ```  
si docker est déjà installé on peut le retirer pour partir d'une installation propre  
```sudo apt-get remove docker docker-engine docker.io```  
installation des packages qui gèrent les certificats  
```sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common```  
ajout du certificat de docker  
```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -```  
ajouter l'acces repo docker d'ubuntu   
```sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"```  
mise à jour du repo   
```sudo apt-get update```  
installation de Docker version Community Edition    
```sudo apt-get install docker-ce```    
ajout de votre user au groupe docker 
```sudo usermod -aG docker votre_user```  ou ```sudo gpasswd -a votre_user docker```  
log out and log in back again de votre shell terminal pour que les changements prennent effet.    
faire  
 ```docker ps``` 
 
## Slide 29
```shell script
  docker run -it --name mycontainer centos /bin/bash
  docker start mycontainer
  docker attach mycontainer
```
##Slide 30 
```shell script
docker run -d --name mytest ubuntu /bin/bash -c "while true; do date ; sleep 5; done"
docker ps
docker logs mytest
docker pause mytest
docker logs mytest
docker unpause mytest
docker logs mytest
```
##Slide 31 
```shell script
# pour arrêter tous les containers qui tournent sur votre machine
docker stop $(docker ps -aq)
# pour détruire tous vos containers
docker rm $(docker ps -aq)
# pour détruire toutes les images 
docker rmi  $(docker images -q)
```

##Slide 32 
```shell script
docker run -it --name test ubuntu
touch {abc,def,ghi}
ls 
ls -alrt
exit
docker diff test
```
##Slide 33
```shell script
docker run -it --name test alpine 
exit
docker commit test alpine:version3
docker images
docker export test > latest.tar
cat latest.tar | sudo docker import - alpine:v1

docker pull busybox:latest
docker images
docker save -o myfile.tar busybox:latest
docker rmi  -f busybox
docker load --input myfile.tar
docker images
```
##Slide 35
```shell script
 docker run -it ubuntu
 clear
 apt-get update
 apt-get -y install python python-pip vim
 pip install flask
 cat > /opt/app.py
```
Inserer le script python suivant:  
```python
# app.py
import os
from flask import Flask
app = Flask(__name__)

@app.route("/")
def main():
    return "Welcome!"

@app.route('/how are you')
def hello():
    return 'I am good, how about you?'

if __name__ == "__main__":
    app.run()
```
et ensuite verifier le bon fonctionnement
```shell script
   vi /opt/app.py
   et sortir de vi
   FLASK_APP=/opt/app.py flask run --host=0.0.0.0
   history
   copier l'historique dans un fichier nomme Dockerfile'
```
## Build webflask image
```shell script
  docker build -t webflask . 
```
## Demarrer le container nomme web 
```shell script
  docker -it -d -p 5000:5000 --name web webflask
```