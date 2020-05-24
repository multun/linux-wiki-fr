Héberger un serveur de jeu
--------------------------

Une très grosse partie des utilisateurs de linux hébergent des services sur leur
machine. Un service est un programme qui démarre avec la machine, et qui est
redémarré en cas de problème.

C'est par exemple pratique pour héberger des serveurs de jeu !

Les services
~~~~~~~~~~~~

La plupart des distributions utilisent ``systemd`` pour gérer les services du
système.

Ouvrez un terminal et saisissez ``systemctl status`` pour lister les services
actifs sur votre machine.

Chaque ligne qui se termine par ``.service`` correspond à un service, et les
lignes immédiatement en dessous sont les processus qui appartiennent au service.


Un système qui ne fait qu'héberger un serveur de jeu aura un status comme
celui-ci :

.. code-block:: none

  ● mamachine
      State: running
       Jobs: 0 queued
     Failed: 0 units
      Since: Wed 2020-03-25 09:37:08 PDT; 14h ago
     CGroup: /
             ├─user.slice
             └─system.slice
               └─monserveurdejeu.service
                 └─4242 /usr/bin/monserveurdejeu


En pratique, il y a beaucoup, beaucoup de services sur une machine !

Pour rajouter un nouveau service, il faut créer un fichier dans le dossier
``/etc/systemd/system``.

Le contenu de ce fichier sert à décrire quoi démarrer avec le service:

.. code-block:: none

  [Unit]
  Description=Un serveur de jeu

  [Service]
  # Quel programme démarrer
  ExecStart=/usr/bin/monserveurdejeu

  [Install]
  # Choisit quand démarrer le service si il est activé.
  # On peut choisir de ne pas démarrer tous les services (pas besoin de démarrer
  # des services graphiques si il n'y a pas d'écran branché par exemple).
  # multi-user correspond à un démarrage normal du système, où plusieurs
  # utilisateurs peuvent s'identifier.
  WantedBy=multi-user.target

On peut ensuite l'activer avec ``systemctl enable monservice``, pour qu'il
démarre tout seul avec la machine, puis le démarrer avec ``systemctl start monservice``.

.. note::

   lorsque vous modifiez le fichier du service, systemd ne prend pas
   immédiatement en compte les changements. Utilisez ``systemctl daemon-reload``
   pour qu'ils soient pris en compte.

La configuration
~~~~~~~~~~~~~~~~

Il n'y a malheureusement pas de format de configuration unifié sous linux.
La configuration dépend du programme dont il est question.

Par contre, tout le monde s'est mis d'accord pour stocker les fichiers de
configuration des services au même endroit: ``/etc``

Si vous créez votre propre service, vous savez où mettre votre fichier :)

L'objectif
~~~~~~~~~~

Votre mission, si vous l'acceptez, et de créer un service systemd qui démarre un
serveur teeworlds !
