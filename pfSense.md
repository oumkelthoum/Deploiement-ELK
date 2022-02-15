## Installation pfsense 

Le logiciel pfSense est un système d'exploitation lui-même et vous ne pouvez pas l'installer sur un autre système d'exploitation. Vous réservez un ordinateur physique entier ou vous le déployez en tant que machine virtuelle dans un système physique tel qu'un serveur. Le déploiement virtuel élimine le besoin d'un ordinateur supplémentaire sur votre réseau.


- Pour la configuration du réseau pour la machine virtuel pfsense on a attribué: 
   --> Adapter 1 :Accés par pont 
   --> Adapter 2 : réseau interne  
et durant l'installation du pfsense on a donne une plage d'addressage de 10.0.0.10 - 10.0.0.254 ce qui est 244 machines
- WAN : 192.168.10.40/24
- LAN : 10.0.0.1/24

- Pour la configuration du machine client qui est ubuntu dans notre cas on a attribuée deux interfaces :
--> interne 
--> NAT

- pour accéder à l'interface du pfsense à partir du machine client http://10.0.0.1 



- virtualbox bar menu : Image->configuration-> interface utilisateur -> sélectionne 

left control + left shift = language 

Install guest additions on ubuntu virtualbox :

- sudo apt update 
- sudo apt upgrade 
- sudo aptinstall build-essential dkms linux-headers-$(uname -r)
uname : Linux 
- Dans la bar de la Machine virtual go to périphérique -> Insert Guest Additions CD Imagesthe RUN 



// dans les étapes pour l'installation du ubuntu cocher le case du mije à jour des logiciels par défauts pour évitee les problèmes des packages 
















diskpart 



 
