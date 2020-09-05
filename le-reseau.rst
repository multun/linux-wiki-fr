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

Apriori, les communications entre ordinateur, c'est pas compliqué: on a des
fils, et on envoie de l'électricité dedans pour transmettre des messages, c'est
comme du morse, mais avec de l'électricité.

Sauf qu'en fait, personne a une ligne directe entre son ordinateur et un moteur de
recherche. En pratique, on a plein de machines branchées ensemble, qui doivent
coopérer pour relayer les messages jusqu'à leur destination.

Y'a plusieurs systèmes de relai de messages sur internet, et les deux plus
importants travaillent ensemble pour transférer vos vidéos de chat: IP, et
ethernet.

C'est un peu deux langues différentes, c'est des manières de communiquer.
En fait, ce sont des protocoles.

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

TODO: bien montrer les MACs

.. slides::

   une slide illustrative

On va commencer par parler du protocole qui est le plus central lorsque votre ordinateur
communique avec votre box, ethernet.

Vous êtes facteur dans un drôle de village:

 - tout le monde ignore les adresses sur le pallier et envoie lettres avec juste
   le prénom du destinataire sur le devant, et le leur derrière
 - les gens ne râlent pas quand ils reçoivent du courrier par erreur, ni quand
   on ouvre leur courrier
 - il n'y a pas de bureau de poste, et pour envoyer du courrier, les gens le
   posent sur leur boite aux lettres
 
Vous êtes ethernet, le nouveau facteur dans ce village, et vous devez livrer
une lettre à destination d'un certain Georges, sans communiquer directement avec
les habitants. Comment vous faites?

Et quand vous ne savez pas où envoyer la lettre, vous êtes obligés de...

A) changer de métier
B) la recopier plein de fois, et d'en déposer une copie devant toutes les maisons du village
C) pris de désespoir, vous toquez à toutes les portes

La bonne réponse est la B! Dans le doute, le message est envoyé à tout le monde.

Heureusement, vous êtes pas obligés de le faire souvent: quand quelqu'un envoie
du courrier, vous notez dans quelle maison vit la personne qui a envoyé la
lettre. Du coup, au fur et à mesure que les gens envoient du courrier, vous
apprenez où livrer les lettres.

Vous vous en doutez sûrement, ethernet fonctionne parreil: dans chaque machine,
il y a une carte réseau, qui a un identifiant unique, assigné lors de sa
fabrication: l'adresse MAC. Il est utilisé comme le prénom dans l'exemple
précédent.

Et puis une machine dans un réseau ethernet a des liens vers d'autres machines,
mais ne sait pas ce qu'il y a au bout, un peu comme le facteur ne sait pas qui
vit dans la maison.

Bon ok, votre ordinateur vient d'arriver sur le réseau, et il veut envoyer un
message.

L'équivalent du village serait un réseau ethernet, qu'on appelle parfois segment.

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

NOTE: exemples pasclairs
NOTE: prénoms to MAC
..
  Au fur et à mesure qu'ils échangent des messages, les ordinateurs du réseau

Les réseaux IP
--------------

Du coup ethernet c'est bien, mais ça a un gros défaut, si on envoie un message à
une machine qu'aucun intermédiaire ne connaît, chaque intermédiaire va être obligé de
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

La bulle à gauche correspond au réseau d'une maison. Il y un
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

TODO: infobulle avec les messages

Imaginons que cette machine de la maison C veuille envoyer un message à cette
machine de la maison A. La machine qui envoie le message a une route vers
la box de sa maison, qui a une route vers la box de la maison A, qui
relaie le message vers sa destination finale.

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

FAIRE UN SCHEMA, refactor, SPACLAIR

Si j'ai parlé d'ethernet et d'IP, c'est que les deux sont très, très largement
utilisés en même temps! En fait, IP ne peut pas fonctionner sans un protocole
comme ethernet.

Ethernet permet à des petits groupes de machines de communiquer ensemble, et IP
permet aux messages de voyager de groupe en groupe jusqu'à leur destination.

Quand une machine envoie un message IP, il est emballé dans un message ethernet
pour voyager dans le segment. Quand le message atteint un routeur intermédiaire,
le message IP est sorti de son packet ethernet, et mis dans un nouveau packet
ethernet à destination du routeur suivant.

En fait, la destination du packet IP ne change pas au fil du trajet: C'est le
packet ethernet qui le contient qui change.

Même dans le même segment ethernet, les machines mettent des messages IP dans
leurs messages ethernet, pour éviter d'avoir un système à part pour communiquer
entre machines d'un même segment.

.. slide::

   Schéma

ARP
---

Mais il y a un problème:
Imaginons qu'un routeur reçoive un message, et qu'il détermine qu'il doive le
transférer à une certaine adresse IP, comme 192.168.0.42. Comment est-ce que le
routeur trouve la destination du message ethernet qui va emballer le message IP?

DHCP
----

Vous vous êtes peut-être demandé plus tôt dans la vidéo qui décide quelle
adresse IP aura une machine. Et bien il y a plusieurs réponses possibles:

 - soit c'est un être humain qui l'a choisie
 - soit c'est une machine qui l'a attribuée

La seconde option est la plus commune pour les utilisateurs finaux; si vous
allez dans les paramètres réseau de votre téléphone, vous aurez probablement la
possibilité de choisir vous-même l'adresse IP de votre téléphone, mais ce n'est
pas l'option par défaut.

Pour découvrir quelle est son adresse IP, une machine va envoyer un message
ethernet à tout le monde sur le réseau, en se présentant et demandant une
adresse.

Une des machines du réseau peut alors répondre, en donnant une adresse IP, une
table de routage, et potentiellement d'autres informations.

DNS
---

Il manque encore un ingrédient: quand vous naviguez sur internet, vous accédez
jamais à un site par son adresse IP. Pourtant, c'est possible! si vous tapez
http://193.17.73.18 dans un navigateur, vous tombez sur prologin.

Les ingénieurs réseau se sont rendus compte assez vite que mémoriser une suite
de chiffre n'est pas exactement pratique: lors de la genèse d'internet, les
utilisateurs s'échangaient un document avec une liste de noms de sites et leur
adresse IP.

Puis, au fur à mesure de la croissance d'internet, la pratique est devenue
intenable, et un autre système a été développé: DNS.

Le protocole est un peu compliqué, et on en parlera plus en profondeur dans une
autre vidéo. DNS permet d'associer des informations à un nom de domaine, comme
lemonde.fr, ou wikipedia.org.

TODO: expliquer ce qu'est un serveur, ou enlever le mot

Pour obtenir ces informations, on contacte un serveur DNS, qui va nous répondre
avec par exemple, l'adresse IP qu'on lui a demandé.

