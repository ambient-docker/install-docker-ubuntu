# install-docker-ubuntu
Install docker on ubuntu 18.04

faire un update du repository des packages ubuntu  
```sudo apt-get update```   
installer les packages htop git et ansible  
```sudo apt-get -y install htop git ```  
si docker est déjà installé on peut le retirer pour partir d'une installation propre  
```sudo apt-get remove docker docker-engine docker.io```  
installation des packages qui gèrent les certificats  
```sudo apt-get - y install apt-transport-https ca-certificates curl software-properties-common```  
ajout du certificat de docker  
```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -```  
ajout du repo docker   
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

