# Maquette
Documentation de la maquette, son fonctionnement, ce qu'elle teste et le résultat de ce test

La maquette de Luminatura a été élaborée pour offrir une **interaction minimale** avec **un seul utilisateur**. Dans ce contexte, on n'utilise qu'une seule plaque pour recevoir les données de la capacitance. À partir de celles-ci, une expérience visuelle, lumineuse et sonore sera créée.

## Composantes essentielles
### Interface utilisateur
* La plaque et son support
* La projection sur le sol
* La projection sur le mur
* L'écairage dans les 3 fleurs
* L'ambiance sonore

### Matériel et Capteurs
**Lié à la capacitance**
* 1 plaque en acier
* 1 minicontrôleur
* 1 trépied
* 2 supports imprimés en 3D
  
**Lié à l'audio**
* 1 haut-parleur

**Suspension et structure centrale**
* Quelques vignes
* 2 lanternes
* 3 fleurs (tissus blanc et jaune ainsi que des fils métalliques)
* Câble métallique en acier inoxydable
* Serre-câbles
* 3 poteaux
* 6 clamps doubles Pro Burger

**Lié à l'éclairage**
* 3 ampoules LED
* 1 transmetteur
* 3 extension pour les lumières

**Lié à la projection**
* 2 projecteurs

**Lié à la gestion**
* 2 ordinateurs

### Logiciel et Scripts
Arduino

* ![arduino_01](https://github.com/user-attachments/assets/fb2f3160-0e9a-4bfe-85da-dd7367858de0)
* ![arduino_02](https://github.com/user-attachments/assets/98586416-2346-40d8-b4fd-1fb0981f1fac)
* ![arduino_03](https://github.com/user-attachments/assets/436a39ad-e6e8-449e-bdde-35cd340b6578)

Puredata

![puredata](https://github.com/user-attachments/assets/15a58055-21bb-4a53-b98e-bf5a1802eb9a)

Reaper (plugdata)

![plugdata_reaper](https://github.com/user-attachments/assets/498680ee-5013-4df6-a187-a7362f703eae)

QLC+

![qlc_01](https://github.com/user-attachments/assets/2be22549-0f59-4cdb-bc2c-105e41b70f57)
![qlc_02](https://github.com/user-attachments/assets/0fb66d4a-3963-44c1-86db-1024aa5deee8)

## Gestion des données et des logiciels

### Gestion des logiciels sur deux ordinateurs
Ordinateur 1:
* QLC+
* Reaper
* Projection au mur

Ordinateur 2:
* Arduino
* Puredata
* Projection au sol

### Les différents ports utilisés
| Port  |  Fonction |
|---|---|
| 10001  | Qlc+  |
| 10002  | TouchDesigner - projection sur le sol  |
| 10003  | Reaper  |
| 10004  | TouchDesigner - projection sur le mur  |

## Les différents prototypes

#### Les fleurs
| Prototype 1  |  Prototype 2 | Prototype 03  | Fleur finale |
|---|---|---|---|
| ![prototype-01](https://github.com/user-attachments/assets/747c9423-8ccd-490e-b17e-11212664e013)  | ![IMG_2596](https://github.com/user-attachments/assets/52870faf-2a4a-47f2-b50a-ef6d72d4afe2)  |  ![IMG_2684](https://github.com/user-attachments/assets/19c9f100-eebc-4046-94e3-1ea79bf9bea3)  |   ![IMG_2712](https://github.com/user-attachments/assets/138edf2f-8060-4c23-8c96-91cf7e2427ce) |

#### La plaque métallique
| Prototype 1  |  Prototype 2 | Prototype 3  |   Plaque finale   |
|---|---|---|---|
| ![IMG_2650](https://github.com/user-attachments/assets/a8e3cfb5-b7d5-4784-a9e2-f3bf43485bbe)  | ![Image (3)](https://github.com/user-attachments/assets/5a681163-cc7e-4ab2-845d-6b757697a32a)  |  ![IMG_2829](https://github.com/user-attachments/assets/a6e8fe81-631c-4c1a-8f09-09745df01d09)  | ![IMG_2838](https://github.com/user-attachments/assets/01d67a14-95b7-462a-8dd1-4e5ccd30baf9) |

## Fonctionnement
### Flux de données et d’interactions
À la base de la maquette, Arduino aquiert les différentes valeurs de la capacitance et les transmet à Puredata. Dans puredata, les données brutes de la capacitance ainsi qu'un booléen 1/0 permettant d'identifier le moment de l'interaction sont utilisés et modifiés. Ces deux données permettent d'affecter l'éclairage des fleurs, l'audio et les deux projections. Celles-ci sont ensuite acheminées à Reaper, Qlc+ et TouchDesigner par l'attribution de ports spécifiques.

```mermaid
graph TD;
    Plaque-->Minicontroleur;
    Minicontroleur-->Arduino;
    Arduino-->Puredata;
    Puredata-->DonneeBrute[Données brutes];
    Puredata-->Donne1-0[Données booléenne 1-0];
    DonneeBrute-->| Port: 10002 |TouchDesignerSol;
    DonneeBrute-->| Port: 10004 |TouchDesignerMur;
    Donne1-0-->| Port: 10001 |QLC+;
    Donne1-0-->| Port: 10003 |Reaper;
    QLC+-->ActivationChaser[Activation du chaser rose par l'intensité lumineuse];
    Reaper-->| Lors d'interraction |DéclenchementSonCourt1[Déclenchement du premier son court];
    DéclenchementSonCourt1-->| Délai de 7 secondes |DéclenchementSonLong[Déclenchement du son long]
    Reaper-->| Plaque inactive |DéclenchementSonCourt2[Déclenchement du deuxième son court];
```

### Mode d'emploi des lumières
#### Association des lumières
*Associer les lumières une à la fois

*Un channel par lumière

Choisir un channel spécifique et allumer la lumière. Dans les 10 prochaines secondes, cliquer trois fois sur le bouton set du transmetteur. La lumière devrait clignoter 3 fois en vert pour démontrer son association.

Pour une seconde lumière, éteindre la première lumière déjà associée et changer de channel sur le transmetteur. Maintenant, allumer la deuxième lumière et refaire le même processus que fait précédemment sur la première lumière.

#### Disassociation des lumières
Éteindre les lumières et les rallumer. Dans les 5 prochaines secondes, appuyer 5 fois sur le bouton set du transmetteur. Les lumières devraient clignoter 10 fois en rouge pour démontrer leur dissociation du transmetteur.

## Gallerie d'images

* ![plaque](https://github.com/user-attachments/assets/62f027cf-6e70-4b67-ae67-3018ea011d71)
* ![ordinateur](https://github.com/user-attachments/assets/7516ee77-bdca-49d4-8ab3-8375a490665b)
* ![stand](https://github.com/user-attachments/assets/fc0e7c8a-3db5-4e45-ae5e-3d0d449cc963)
* ![projection](https://github.com/user-attachments/assets/46979407-bc4a-4576-be79-92e1c6e9e297)


## Vidéo du la maquette en action

<iframe width="560" height="315" src="https://www.youtube.com/embed/9Ty8B9qVx1c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
