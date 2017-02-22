# RadioBoard

Design d'une carte électronique permettant de d'échanger des messages et de localiser les robots

## Définition des acteurs

![radio global](/radio-global.png)

On distingue 3 types d'acteurs aux besoins différents :

* les robots, où la radio se comporte comme un esclave piloté par le raspberry pi et autres composants
* les balise sur les robots adverses, où la radio est indépendante et doit envoyer les mesures aux robots
* les balises fixes, où la radio est indépendante et peut communiquer avec un ordinateur pour le debug

## Vue système

### Système robot

![archi robot](/architecture-robot.png)
