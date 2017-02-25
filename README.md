# RadioBoard

Design d'une carte électronique permettant de d'échanger des messages et de localiser les robots

## Définition des acteurs

![radio global](/Specs/radio-global.png)

On distingue 3 types d'acteurs aux besoins différents :

* les robots, où la radio se comporte comme un esclave piloté par le raspberry pi et autres composants
* les balise sur les robots adverses, où la radio est indépendante et doit envoyer les mesures aux robots
* les balises fixes, où la radio est indépendante et peut communiquer avec un ordinateur pour le debug

Pour des raisons d'efficacité, il a été décidé de ne concevoir qu'une seule carte, adaptée aux besoins de tous les acteurs.

## Vue système

### Système robot

![archi robot](/Specs/architecture-robot.png)

Il est nécessaire de fournir 3 ports :
* Un port esclave sur le bus I2C principal du robot, permettant la communication avec le Raspberry Pi
* Un port esclave SPI pour une liaison direct rapide à faible latence avec la carte de contrôle des moteurs
* Un port série pour ouvrir un terminal série à distance sur le Raspberry Pi contrôlé depuis une balise fixe en cas de perte de la connexion WiFi (environnement difficile pendant la coupe)

Par ailleurs, l'alimentation qui sera fournie à la carte sera du 5V (en raison de la consommation importante des Decawaves, il est plus raisonnable de ne pas tirer sur le 3.3V du Raspberry Pi), elle devra donc être abaissée localement.

### Système balise

![archi balise](/Specs/architecture-balise.png)

Dans les balises (fixes et sur les robots adverses), la carte radio est l'unique carte, et n'est accompagnée que d'une batterie. Elle doit donc être autonome.

La faisabilité d'un système interne de recharge doit être étudié. Dans tous les cas, le système doit pouvoir détecter la fin de décharge de la batterie afin d'éviter la destruction de celle-ci.

## Contraintes

#### RC1 Placement du module radio
Pour fonctionner correctement, le module radio DWM1000 doit être placé conformément aux contraintes de la datasheet du DWM1000 page 17.

#### RC2 Taille de la carte
Afin de pouvoir être embarqué dans les balises, la carte devra avoir des dimensions maximales de 70mmx70mm. De plus, il est important de minimiser la taille de la carte pour des raisons d'efficacité budgétaire. Il faut également prévoir le placement des batteries pour les balises, afin que le système total rentre dans un pavé de 80x80x80mm comme spécifié dans le règlement de la coupe de France de robotique.

#### RC3 Placement des connecteurs
Tout les connecteurs devront être placés de telle sorte qu'un câble connecté ne puisse pas se mettre dans le chemin du signal radio entre deux modules.

#### RC4 Programmation et debug de la carte
La programmation et le debug des cartes sera fait avec les sondes J-link du club en SWD et devra utiliser un connecteur comme [celui-ci](http://fr.farnell.com/samtec/shf-105-01-l-d-sm/embase-male-1-27mm-2x5-voies/dp/1885915).

#### RC5 Alimentation de la carte
L'alimentation de la carte se fera dans les robots en 5VDC et dans les balises directement depuis les batteries sans composant extérieur.
