Le système de fichier
=====================

L'organisation hiérarchique
---------------------------

Avec linux, les fichiers ne sont pas organisés de la même manière qu'avec
Windows.

Avec Windows, chaque volume de stockage a une lettre assignée. On peut ensuite
référencer les données sur le disque comme suit: ``MONDISQUE:\dossier\fichier``

Linux reprend une approche en fait bien plus populaire dans le milieu des
système d'exploitation que celle utilisée par Windows:

 - un volume est choisi au démarrage comme étant le volume principal (aussi
   appelé volume racine)
 - on référence le contenu du volume racine avec ``/mondossier/monfichier``
 - il est ensuite possible de commencer à utiliser d'autres volumes en les
   faisant correspondre à un dossier existant.

On peut par exemple faire en sorte que le contenu du dossier
``/stockage/disque_externe`` soit stocké sur un disque externe, et que tout le
reste de l'arborescence soit stocké sur le disque principal.
