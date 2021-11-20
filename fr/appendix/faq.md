# Résolution des problèmes

## Problème 1 : `poppy.local` ne se charge pas (procédure de diagnostic)

C'est l'erreur la plus manifeste que vous n'arrivez pas à utiliser votre robot : taper `http://poppy.local` dans votre navigateur aboutit à une erreur indiquant que le site web ne peut être chargé. Par exemple :

![La page n'existe pas](../assembly-guides/ergo-jr/img/IHM/webpage_not_available.jpg)

La difficulté de cette erreur est qu'elle peut avoir de multiples causes. Mais pas d'inquiétude, voici une procédure pour vous aider à trouver la source du problème :

### I. Faire un test ping
Un "ping" est tout simplement une tentative de connexion au robot, qui répondra avec un "pong". Ce qui permet ensuite de mesurer diverses statistiques de temps de communication.

1. Connectez votre robot avec un cable Ethernet soit directement ou au travers d'un routeur/box, et branchez l'alimentation pour que votre robot démarre
2. Ouvrez un terminal : sur Windows pressez la touchez "Windows" ç gauche de la barre d'espace et tapez "cmd" dans le champs de recherche qui apparait puis validez par Entrée. Sur GNU/Linux ou OSX, une application spéciale nommée Terminal peut facilement être trouvée dans la liste des applications ou les menus
3. Vous optenez une fenêtre, généralement sur fond sombre et un invite de commande qui mentionne votre nom d'utilisateur et le nom de votre ordinateur. A la suite de l'invite de commande, tapez `ping poppy.local` puis appuyez sur Entrée.
4. En réponse, chaque second, une nouvelle ligne s'affiche à l'écran, telles que :

![Test ping réussi](/img/ping.png)

Selon votre système d'exploitation et votre réseau, le look de la fenêtre, les adresses IP et les délais peuvent largement varier par rapport à la capture d'écran ci-dessus. Le plus improtant est d'identifier si chaque ligne mentionne des délais de communication en millisecondes. Si oui, alors le test ping est **réussi**, comme dans la capture d'écran. Dans ce cas, l'adresse IP entre parenthèses à côté du nom du robot est l'adresse IP actuelle de votre robot. Attention, cette adresse IP peut changer d'un jour à l'autre alors que `poppy.local` ne change jamais, à moins que vous changiez le nom de votre robot dans les paramètres.

Si le test est réussi, passez à la section **II.A**. Sinon, une erreur est probablement affichée à la place, indiquant que la tentative de communication a échoué, dans ce cas consultez **II.B.**.

Avec Windows, un test ping s'arrête automatiquement après 4 lignes. Sur GNU/Linux et OSX, de nouvelles lignes s'affichent sans arrêt. Vous pouvez les arrêtez en pressant simultanément Ctrl + C ou bien en fermant la fenêtre. 

### II.A. Si le test ping réussit

Si le test ping réussit mais que vous ne pouvez toujours pas charger `http://poppy.local` dans votre navigateur, alors le problème vient du côté du navigateur.

1. Vérifiez que vous n'oubliez pas le préfix `http://`. Ce préfixe s'assure qu'une connexion normale au robot est établie. Les navigateurs modernes forcent parfois une connexion sécurisée en le remplaçant par `https://`. Cependant les connexion sécurisées ne fonctionnent que lorsque vous êtes sur Internet.
2. Vous pourriez rencontrer des problèmes de cache, appuyez sur Ctrl + Maj + R dans votre navigateur pour forcer le rechargement de la page sans cache.
3. Essayez un autre navigateur : Mozilla Firefox, Chromium, Safari, Opera, Microsoft Edge, Google Chrome...
4. En dernier recours, il est possible que le logiciel Poppy ne parvienne pas à démarrer, dans ce cas il est recommandé de [re-flasher votre carte SD](../installation/burn-an-image-file.md).

### II.B. Si le test ping échoue

Si le test ping échoue vous rencontrez un problème de communication : votre ordinateur n'arrive pas à contacter le robot !
1. Déconnectez l'alimentation du robot
2. branchez-la de nouveau en prêtant une attention particulière aux LED rouges et vertes de la Raspberry Pi :

**La LED `PWR` (Power) doit être rouge en continu 🔴** et **la LED `ACT` (activity) verte 🟢 doit vaciller de manière irrégulière pendant environ 45 secondes**, signifiant que le robot est en train de démarrer. Continuez avec A, B, C, ou D selon votre situation :

A. Si `PWR` n'est pas rouge fixe 🔴 : vous avez un problème d'alimentation. Sur un robot Ergo Jr, vous pourriez avoir mal enfiché la carte Pixl, vérifiez que vous avez bien respecté [la procédure d'assemblage électronique](../assembly-guides/ergo-jr/electronic-assembly.md). Sinon, votre carte Pixel ou votre Raspberry Pi pourraient être défectueuse. Tentez d'échanger ces composants avec d'autres robot si vous en avez, ou contactez votre fournisseur.

B. Si la LED verte `ACT` reste éteinte, alors le systèem sur la carte SD est probablement endommagé, ou bien la carte SD elle-même, ou bien la Raspberry Pi. Testez d'abord de [re-flasher la carte SD](../installation/burn-an-image-file.md), ensuite essayez de flasher et utiliser une autre carte SD, et en dernier recours essayez une autre Raspberry Pi.

C. Si la LED verte `ACT` 🟢 clignote de façon régulière comme une séquence de flashs longs et courts, cette séquence vous donne des indices sur l'origine du problème, veuillez dans ce cas consultez [la documentation appropriée](https://www.raspberrypi.org/documentation/configuration/led_blink_warnings.md).

D. Si la LED verte `ACT` 🟢 vacille de manière **irrégulière** pendant environ 45 secondes, puis s'éteint quasi homris des flash ponctuels, cela signifie que le robot démarre normalement. Votre problème dans ce cas est d'ordre réseau. Le mode de connexion que vous utilisez (wifi, Ethernet direct, Ethernet via un routeur/box, ou hostpot) pourrait ne pas fonctionner dans votre situation. Une bonne idée dans ce cas est de se replier sur la méthode de conneixon la plus simple possible : avec un câble Ethernet au travers d'un routeur ou d'une box, ce qui nécessite 2 câbles Ethernet : l'un de votre robot à votre routeur/box, l'autre de votre ordinateur à votre routeur/box. Ensuite suivez de nouveau la procédure de diagnostic.

## Problème 2 : Les mouvements de mon robot sont saccadés

Ceci est souvent dû à des câbles déteriorés. C'est d'autant plus flagrant si vous sentez en les manipulant que les câbles sont rigides par rapport à des câbles neufs, alors qu'ils devraient être souples. Ceci cause des problèmes de communication. Changez les câbles par des câbles neufs.

## Problème 3: Je visualize des erreurs fréquentes à propos de la boucle "pos/speed/load sync loop"

La boucle "pos/speed/load sync loop" est la routine du robot responsable de la communication avec les moteurs. Toute erreur de cette routine peut survenir d'un signal altéré en provenance des moteurs.

La plupart du temps, de telles erreurs sont ponctuelles et sont résolues après un reboot des moteurs (débrancher puis rebrancher l'alimentation des moteurs) ou une simple reconnexion logicielle (en redémarrant l'API du robot via les boutons prévus dans l'interface graphique ou en ré-établissant une connexion via Jupyter si vous utilisez Python).

Si ces erreurs sont trop fréquentes, voici quelques pistes pour vous aider à identifier (et ensuite régler) le problème :

* Remplacez le bloc secteur par un nouveau. Utilisez un adaptateur secteur qualitatif, ceux de qualité moyenne peuvent générer un courant instable qui pourrait interférer avec la communication électronique
* Remplacez les câbles de connexion des moteurs (cf le problème 2 pour plus d'information)

Des problèmes de communicaiton similaires peuvent déclencher des exceptions de type `DxlError`. Avec Poppy Torso ou Humanoid, vous pouvez essayer de [couper le fil central du cable directement connecté à l'USB2AX](../en/assembly-guides/poppy-humanoid/warnings.html#warning-5-your-robot-is-sensitive-to-interferences).

## Problème 4: Les moteurs ne sont pas détectés

Si certains moteurs ne sont pas détectés, vérifiez d'abord qu'ils sont configurés avec le bon protocole : Protocole 2.0 pour XL-320 mais 1.0 pour tous les autres modèles. Vous pourriez avoir besoin de réinitialiser le firmware de vos moteurs non détectés également. Consultez la [documentation Dynamixel](https://emanual.robotis.com/docs/en/dxl/protocol2/) pour réinitialiser ou changer le protocole avec Robot Plus ou Dynamixel Wizard.

Vous pouvez utiliser [Herborist](https://github.com/poppy-project/herborist#herborist) pour scanner tous les motors sur le bus et détecter automatiquement leur ID et baudrate.

Si le problème survient toujours, vous pouvez utiliser le mode DEBUG pour obtenir plus de détails. Il nécessite d'utiliser Python :

```python
import logging, sys
logging.basicConfig(stream=sys.stderr, level="DEBUG")

# Ensuite connectez-vous à vos moteurs via la méthode la plus appropriée, par exemple :
import pypot.dynamixel.io
pypot.dynamixel.io.DxlIO("COM3", baudrate=57600).scan()

import poppy_torso
poppy_torso.PoppyTorso()
```

Vous verrez apparaitre les messages de déboguage dans votre terminal, incluant les paquets envoyés aux moteurs (et les réponses des moteurs, s'il y en a).


## Problème 5 : Mon robot fait des mouvements bizarres ou s'auto-collisionne

Si votre robot fait des mouvements qui ne correspondent pas à ce que vous attendez ou qui font que poppy s'auto-collisionne, c'est probablement que vous avez assemblé votre robot à l'envers. Reprenez chacune des étapes une par une et vérifiez attentivement que votre les pièces de votre robot sont en tout point positionnées identiquement au photos ou schémas. Il est assez facile de se tromper et d'obtenir un robot qui a l'air bien assemblé, alors qu'il ne l'est pas.

## Problème 6 : Quel est le mot de passe SSH par défaut de mon robot ?

Un mot de passe est demandé exclusivement pour l'accès à votre robot via SSH, pour les utilisateurs avancés. Avec l'image Poppy standard, le nom d'utilisateur est `poppy` et son mot de passe est `poppy`. Avec l'image ROS, le nom d'utilisateur est `pi` et son mot de passe est `raspberry`.

## Problème 7 : les fichiers STL que je télécharge semblent corrompus

Sur les dépôts Poppy, les ressources lourdes -dont les fichiers STL- sont stockées via [Git Large File Storage (LFS)](https://git-lfs.github.com/). A ce titre, il est nécessaire d'utiliser Git LFS pour les télécharger.

Certains clients git prennent en charge LFS, d'autres non ([y compris le bouton `Download ZIP` de Github](https://github.com/git-lfs/git-lfs/issues/903)). Dans ce dernier cas les fichiers que vous téléchargerez sembleront corrompus et de petite taille (une centaine d'octets). 

**Solution :** Veuillez [télécharger un client compatible LFS](https://github.com/git-lfs/git-lfs/releases/latest), l'installer, puis utiliser ce client pour récupérer les fichiers STL des dépôts Poppy.
