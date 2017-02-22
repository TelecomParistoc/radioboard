# RadioBoard

Design d'une carte électronique permettant de d'échanger des messages et de localiser les robots

## Définition des acteurs

![radio global](/radio-global.png)

On distingue 3 types d'acteurs aux besoins différents :

* les robots, où la radio se comporte comme un esclave piloté par le raspberry pi et autres composants
* les balise sur les robots adverses, où la radio est indépendante et doit envoyer les mesures aux robots
* les balises fixes, où la radio est indépendante et peut communiquer avec un ordinateur pour le debug

Pour des raisons d'efficacité, il a été décidé de ne concevoir qu'une seule carte, adaptée aux besoins de tous les acteurs.

## Vue système

### Système robot

![archi robot](/architecture-robot.png)

Il est nécessaire de fournir 3 ports :
* Un port esclave sur le bus I2C principal du robot, permettant la communication avec le Raspberry Pi
* Un port esclave SPI pour une liaison direct rapide à faible latence avec la carte de contrôle des moteurs
* Un port série pour ouvrir un terminal série à distance sur le Raspberry Pi contrôlé depuis une balise fixe en cas de perte de la connexion WiFi (environnement difficile pendant la coupe)

Par ailleurs, l'alimentation qui sera fournie à la carte sera du 5V (en raison de la consommation importante des Decawaves, il est plus raisonnable de ne pas tirer sur le 3.3V du Raspberry Pi), elle devra donc être abaissée localement.

### Système balise

T.B.D.

## Contraintes

T.B.D.
