---
title: Dump d'un routeur
---


![[Pasted image 20231023194012.png]]

## Étape 1 : Identification des Pads de Debug et du Protocole

Notre première étape consiste à trouver les pads de debug et à déterminer le protocole de communication, qui peut être SWD, JTAG, ou UART.

## Étape 2 : Test de l'UART - Multimètre 

Nous avons repéré 4 broches sur le PCB, ce qui suggère la présence d'une interface UART. Pour confirmer cela, nous utilisons un voltmètre en mode Continuité en reliant une borne à la masse (GND) et en vérifiant quelles broches émettent un signal sonore. La première broche à émettre le signal sonore est le GND.

![[Pasted image 20231023194119.png]]
## Etapes 3 : Utilisation d'un Analyseur Logique

Nous poursuivons en confirmant les broches à l'aide d'un analyseur logique. Le fil noir est le GND, et nous identifions les autres broches dans l'ordre : gris (0), marron (1), rouge (2). 

Nous alimentons le PCB et capturons la séquence de boot à l'aide du logiciel de l'analyseur logique (DSView (propriétaire)). Sur les 3 broches restantes, nous identifions RX (réception) et VCC (tension constante), ce qui nous conduit à supposer que TX (transmission) ne transmet rien.

![[Pasted image 20231023194135.png]]
![[Pasted image 20231023194149.png]]

À la fin de la capture (1 min), nous ajoutons un décodeur que nous réglons comme UART selon notre hypothèse initiale. Malgré nos tentatives de changement du "Baud rate" (vitesse de transmission) avec des valeurs courantes comme 115200 ou 9600 baud, nous n'obtenons pas de données intelligibles, remettant ainsi en question notre hypothèse de départ.

## Étape 4 : Connexion aux Broches

Nous utilisons un Arduino, un connecteur FTDI pour établir la connexion aux broches identifiées. Ensuite, nous ouvrons un terminal sur notre ordinateur et nous utilisons la commande suivante :

`screen /dev/ttyACM0 115200`

![[Pasted image 20231023194208.png]]

Nous réussissons à accéder au routeur en tant qu'utilisateur "root" !

![[Pasted image 20231023194253.png]]
![[Pasted image 20231023194227.png]]
## Étape 5 : Extraction du Firmware

Étant donné que le routeur utilise un système Linux embarqué, nous souhaitons extraire le système de fichiers (FileSystem), mais si cela n'était pas un système Linux, nous aurions opté pour la récupération du binaire. On se connecte à la box en wifi et nous tentons d'utiliser des binaires déjà présents pour exfiltrer des fichiers, mais cela échoue. Les serveurs FTP ne fonctionnent pas non plus. Nous optons pour la récupération du système de fichiers en utilisant netcat avec la commande suivante :

`cat /dev/mdblock{0..7} |  ./netcat-static-armel IP_SERVER PORT_SERVER`

Voici les fichiers récupéré

Nous obtenons les fichiers du routeur, parmi lesquels le fichier `5_filesystem.image` et le `1_urlader.image` (bootloader) sont particulièrement intéressants.