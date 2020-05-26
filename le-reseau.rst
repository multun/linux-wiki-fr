.. slide::

   slide titre

Bienvenue dans l'univers mystérieux du réseau.
Si vous vous demandez par quelle magie vous pouvez envoyer des messages à
l'autre bout du monde en moins d'une seconde, cette série est pour vous.

Ça faisait partie des trucs les plus mystérieux pour moi il y a quelques années,
et je tacherai de faire de mon mieux pour partager mon expérience.

Le réseau
=========

.. slides::

   carte d'un réseau

Le réseau dont on parle ici, c'est internet. Un énorme réseau de machines qui
s'échangent des messages, connectées entre elles par des liens.

.. slide::

   machine connectée à une box

Si j'ouvre un navigateur et je tape quelque chose dans un moteur de recherche,
ma requête va parvenir au moteur, qui va me renvoyer une réponse. Et
aujourd'hui, on va essayer de comprendre comment ma requête parvient au moteur,
et comment parviens la réponse.

Si j'avait mon ordinateur et le moteur de recherche directement branchés
ensemble, ça serait pratiquement aussi simple qu'un téléphone yaourt:
on enverrait le message sous la forme d'un signal électrique dans le lien,
et le moteur de recherche pourrait le recevoir.

Sauf qu'on a pas du tout ça, vu que mon ordinateur est pas directement branché
au moteur de recherche. On a plein de machines branchées ensemble, qui doivent
coopérer pour relayer le message jusqu'à sa destination.

Y'a plusieurs systèmes de relai de messages sur internet, et les deux plus
importants travaillent ensemble pour transférer vos vidéos de chat: IP, et
ethernet.

Les messages
------------

.. slide::

   un pakay

Peu importe le système, chaque message contient l'adresse de l'émetteur, du
destinataire, et un contenu. Le contenu est d'une taille limitée, un peu comme
les messages sur twitter. Histoire de compliquer les choses, un message IP
s'appelle un packet, et un message ethernet une trame.

Les réseaux ethernet
--------------------

.. slides::

   une slide illustrative

On va commencer par parler du protocole qui est le plus central lorsque votre ordinateur
communique avec votre box, ethernet.

Imaginez que vous venez d'entrer à l'université, et que personne ne se connaît.
C'est le premier jour, et les élèves doivent distribuer eux-mêmes les papiers
administratif.

Vous prenez un papier, et il est à destination de George Abitbol. Sauf que vous
connaissez personne, du coup vous êtes obligés de chercher George en annonçant
son nom un peu partout.

Vous livrez quelques autres papiers de la même manière, et surprise, vous tombez
sur un autre papier destiné à George.

Cette fois, vous savez exactement comment contacter George :)

Et bien les réseaux ethernet fonctionnent un peu parreil!

Déjà, chaque carte réseau a un identifiant unique, assigné lors de sa
fabrication: l'adresse MAC. Il est utilisé comme le prénom dans l'exemple précédent.

Et puis comme un élève dans une nouvelle classe, de base, dans un réseau ethernet,
les ordinateurs ne savent pas avec qui ils peuvent communiquer. Chaque
ordinateur est en lien avec un certain nombre d'autres machines, sans vraiment
savoir qui est au bout de chaque lien!

Bon ok, votre ordinateur vient d'arriver sur le réseau, et il veut envoyer un
message.

Il envoie le message par son seul lien, et la machine au bout du fil le reçoit.
Le message est pas pour elle, du coup elle le transfère, mais elle a plusieurs
choix, et ne sait pas vers où aguiller le message!

Du coup, l'intermédiaire fait des copies du messages, et en envoie une par
chemin possible.

Chacun de ces messages va parvenir à une autre machine, qui va faire la même chose.

Maintenant, admettons que cet ordinateur, ici, en bas, veuille envoyer un
message au mien.

Il envoie son message, et quand le premier intermédiaire le reçoit, il se
souvient de par où contacter ma machine, vu qu'elle a transféré un de ses
messages juste avant. Du coup elle le transfère directement au bon destinataire.

Et chaque machine qui transfère un message fait parreil: quand une machine
veut envoyer un message, si elle n'a jamais vu de message provenant du
destinataire, elle l'envoie partout dans le doute, sinon elle l'envoie d'où le
dernier message du destinataire venait.

..
  Au fur et à mesure qu'ils échangent des messages, les ordinateurs du réseau

Les réseaux IP
--------------

Du coup ethernet c'est bien, mais ça a un gros défaut, si on envoie un message à
une machine que personne connaît, chaque intermédiaire va être obligé de
l'envoyer à tous ses voisins pour s'assurer que le message arrive à destination.
Ça veut dire que si le réseau comporte un million de machines, et qu'on envoie un
message à un destinataire inconnu, tout le monde sur le réseau va recevoir le
message.

En plus, dans un réseau ethernet, on peut envoyer des annonces. Une annonce,
c'est un message qui est destiné à toutes les machines du réseau ethernet!
Et c'est plutôt fréquent.

Et tout ça, ça pose problème: si le réseau est trop gros, les machines du réseau
passeront beaucoup trop de temps à recevoir des messages destinés à tout le monde.

La source du problème est qu'une adresse MAC ne dit rien sur la position d'une
machine dans le réseau. Quand une machine reçoit un message à transférer et ne
connaît pas le destinataire, elle est bien obligée de l'envoyer partout dans le
doute.

Alors que dans un réseau IP, les adresses sont organisées pour rendre les choses
plus faciles, comme des adresses postales.

Quand vous envoyez une lettre au 16 Rue du chat qui Danse à Bagneux, votre
bureau de poste a pas besoin de savoir où est la Rue du chat qui danse
exactement, il se contente d'envoyer la lettre dans la région où se trouve
Bagneux, qui va l'envoyer au bureau de poste de Bagneux, qui va la faire livrer
dans la bonne rue.

Et bien les réseaux IP, ça fonctionne un peu parreil.

Déjà, une adresse IP, ça ressemble à ça:
4 nombres de 0 à 255

On pourrait imaginer que le premier nombre correspond au pays, le second à la région, le
troisième de ville, et ainsi de suite. En pratique c'est un peu plus compliqué,
mais l'idée est là.

Allez, un exemple.

.. slide::

   réseau maison

Dans ce schéma, chaque bulle est un réseau. Pour l'instant,
on va partir du principe que les machines de chaque réseau peuvent communiquer
entre elles, et on parlera plus tard de comment.

La bulle à gauche correspond au réseau d'une maison. Il y a deux
ordinateurs et une box, et on voit que la box est dans une position
particulière: elle est à cheval entre deux réseaux.

Le premier réseau c'est celui de la maison, qui a des adresses en 1.2.3. quelque
chose. À droite on voit aussi un bout du second réseau, que la box va utiliser
pour communiquer avec le fournisseur d'accès internet. Ici, la box a pour
adresse 1.2.10.3 dans le réseau du fournisseur.

Quand une machine veut transmettre un message dans un réseau IP, y'a deux cas de
figure: soit la destination est dans le même réseau et on peut directement la
contacter, soit elle est ailleurs. Dans ce cas, en fonction de l'adresse de
destination, un intermédiaire va être choisi pour relayer le message.

Par exemple, si l'ordinateur veut contacter la box, il peut le faire directement.
Par contre, si il veut contacter un machine en dehors du réseau, comme un site
internet, il va faire passer ses messages par la box.

Et pour choisir quoi faire exactement, on utilise une table de routage!
En gros, c'est une liste de règles comme ça:

- si la destination commence par 1.2.3, le message passe par le lien truc
- si le message commence par autre chose, on l'envoie via 1.2.3.1

Chaque règle s'appelle une route, et c'est peut-être le concept le plus
important d'internet.

Là c'était un petit exemple, mais ça marche aussi à très grande échelle:

.. slide::

   réseau ville

Ce schéma, c'est la carte du réseau d'une petite ville: il y a deux quartiers, le
quartier rouge a deux maisons, et le quartier bleu en a 3. Chaque point est une
machine, chaque rond barré est un routeur, et chaque bulle est un réseau. Les
routeurs avec des lettres sont les boxs dans des maisons, c'est deux là c'est les routeurs de
quartier, et celui tout en haut c'est le routeur de la ville. Ici chaque routeur
sert de passerelle entre le réseau dont il est responsable et le reste.

à gauche du schéma, il y a les adresses des machines pour chaque réseau de la carte.

Et vous allez voir qu'avec du routage bien fait, tout ce beau monde peut
communiquer sans problème.

Imaginons que cette machine de la maison C veuille envoyer un message à cette
machine de la maison A. La machine qui envoie le message aurait une route vers
la box de sa maison, qui aurait une route vers la box de la maison A, qui
relaierait le message vers sa destination finale.

Si une machine en dehors de la ville veut contacter une machine de la maison E,
on va d'abord passer par le routeur central de la ville, puis par le routeur du
quartier rouge, puis par la box de la maison E, avant d'enfin arriver à destination.

Comme autre exemple, si la box de la maison D vent envoyer un message à la
box de la maison B, le message va être routé vers le routeur du quartier rouge,
puis vers le routeur du quartier bleu, puis directement envoyé sur le réseau du
quartier bleu.

Ça sera sûrement plus clair avec une vraie table de routage: j'ai choisi
d'écrire celle du routeur du quartier rouge. Chaque ligne commence par une
description des adresses pour lesquelles la route s'applique, et se termine par
le chemin que la route décrit.

Si plusieurs routes correspondent, on choisit la plus précise. Par exemple, si
on envoie un message à 1.1.1.1, la première et la deuxième route correspondent,
mais la seconde est plus spécifique, du coup le message partira vers le routeur
du quartier bleu.

Une route "via" décrit un chemin qui passe par un intermédiaire, et une route
"sur" décrit un chemin direct.

Ethernet et IP
--------------

Si j'ai parlé d'ethernet et d'IP, c'est que les deux sont très, très largement
utilisés en même temps! En fait, IP ne peut pas fonctionner sans un protocole
comme ethernet.

Ethernet permet de communiquer simplement à courte distance, et de distinguer
les machines les unes des autres. IP permet de communiquer efficacement peu
importe le nombre de machines.

En général, chaque machine du réseau a à la fois une adresse MAC, et une adresse
IP.

Encore plus fou, la plupart des messages échangés sont des messages ethernet
contenant un messageftination du sous réseau, il est embalé dans un
message ethernet à destination de la machine en connection avec le reste du monde.

Histoire de ne pas avoir un système à part à pour les messages qui ne quittent
pas le sous réseau, on envoie généralement aussi des messages IP embalés dans un
message ethernet.

.. slide::

   Schéma

Quand un message à pour destination finale une machine du même réseau ethernet,
l'adresse de destination MAC et IP désigne la même machine.

Et au final, c'est vrai qu'il y a deux adresses pour la même machine, mais elles
ont pas le même rôle, l'adresse ip c'est un peu comme une adresse postale, elle
donne des infos sur ou est ce que la machine se situe dans le réseau, là ou
l'adresse mac c'est plus comme un prénom.

Et encore une fois, c'est un peu comme dans la vraie vie. Quand vous envoyez un
message ip à certaines destinations, vous savez directement comment le faire
parvenir à destination, car vous êtes sur place. Par contre, pour certains
messages, vous préférez faire confiance à quelqu'un d'autre, un peu comme on
fait confiance à la poste pour faire parvenir nos lettres à destination.

Quand le bureau de poste reçoit la lettre, il effectue le même raisonnement:
il délivre directement le message si possible, et le transfère à un
intermediaire susceptible de connaître la suite du chemin.
s
Pour savoir quelles adresses sont à portées, et à qui faire confiance quand
un réseau n'est pas directement accessible, chaque machine utilise une liste de
règles:
sa table de routage.

Et une table de routage, ça ressemble un peu à ça. Chaque règle s'applique
seulement si elle la destination commence par un certain préfixe, et prend la
décision de quoi en faire:

 - considérer que la destination est directement joignable avec ethernet
 - passer par un intermédiaire
