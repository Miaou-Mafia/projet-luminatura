# Maquette

La maquette de Luminatura a été élaborée pour offrir une **interaction minimale** avec **un seul utilisateur**. Dans ce contexte, on n'utilise qu'une seule plaque pour recevoir les données de la capacitance. À partir de celles-ci, une expérience visuelle, lumineuse et sonore sera créée.

## Composantes essentielles de la maquette
### Interface utilisateur
* La plaque en acier
* Le support (support des hauts-parleurs)
* La projection sur le sol 
* La projection sur le mur
* L'écairage dans les 3 fleurs
* L'ambiance sonore
* Effets sonores

### Matériel et Capteurs
**Lié à la capacitance**
* 1 plaque en acier
* 1 minicontrôleur Atom M5
* 3 résisteurs
* 1 Cable Ethernet
* 1 Ruban adhésif métalique
* 1 Cable en acier
* 1 trépied
* 2 supports imprimés en 3D


**Lié à l'audio**
* 1 haut-parleur
* 1 Cable DMX
* 1 Carte de son

**Suspension et structure centrale**
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
* 1 projecteur qui se projete au sol
* 1 projecteur qui se projete au mur

**Lié à la gestion**
* 1 ordinateur portable
* 1 PC

### Logiciels et Scripts

#### Arduino

* ![code_arduino_01](https://github.com/user-attachments/assets/fb2f3160-0e9a-4bfe-85da-dd7367858de0)
* ![code_arduino_02](https://github.com/user-attachments/assets/98586416-2346-40d8-b4fd-1fb0981f1fac)
* ![code_arduino_03](https://github.com/user-attachments/assets/436a39ad-e6e8-449e-bdde-35cd340b6578)

Le code Arduino mesure la capacitance de l’utilisateur, qui correspond à la capacité du corps à stocker une charge électrique. Cette valeur est limitée à un maximum de 1000 pour assurer une calibration cohérente. Une plaque en acier sert de capteur et détecte les variations de capacitance lorsque l’utilisateur la touche la plaque en acier. Les données captées sont transmises via le port 8001, utilisant une connexion réseau Ethernet pour la communication. PureData reçoit ces informations et les utilise pour générer des interactions sonores et visuelles en temps réel.

#### Puredata

![code_puredata](https://github.com/user-attachments/assets/15a58055-21bb-4a53-b98e-bf5a1802eb9a)

Le code PureData collecte les données brutes d'Arduino en fonction de la capacitance de l'utilisateur. Ensuite, un effet de transition fluide est appliqué pour lisser les valeurs. Puis, il envoie deux types de données : les données brutes et les données booléennes. Ces données sont transmises à des ports spécifiques pour chaque logiciel sur le PC.

#### Reaper (plugdata)

![code-plugdata-reaper](https://github.com/user-attachments/assets/11b8adae-cce2-4c94-9552-f15734bc7a1e)
![delay-sans-delay-patch](https://github.com/user-attachments/assets/45a7c920-410d-42d8-8386-9edc060035f5)

Les données booléennes de PureData sont envoyées à Reaper pour qu'il puisse déclencher et éteindre des sons à partir de l'OSCParse.

#### QLC+

![configuration_qlc_01](https://github.com/user-attachments/assets/2be22549-0f59-4cdb-bc2c-105e41b70f57)
![configuration_qlc_02](https://github.com/user-attachments/assets/0fb66d4a-3963-44c1-86db-1024aa5deee8)

Les données booléennes sont utilisées pour déclencher 3 ampoules qui sont connectées chacune à un canal différent sur le transmetteur.

| Ampoules   | Canal    |
| ---------- | -------- |
| Ampoule 01 | Canal 01 |
| Ampoule 02 | Canal 02 |
| Ampoule 03 | Canal 03 |

## Gestion des données et des logiciels

### Gestion des logiciels sur deux ordinateurs
Ordinateur 1 (PC):
* QLC+
* Reaper
* Projection au mur

Ordinateur 2 (Ordinateur portable):
* Arduino
* Puredata
* Projection au sol

### Les différents ports utilisés
| Port  | Fonction                              |
| ----- | ------------------------------------- |
| 10001 | Qlc+                                  |
| 10002 | TouchDesigner - projection sur le sol |
| 10003 | Reaper incluant le fichier Plugdata   |
| 10004 | TouchDesigner - projection sur le mur |

## Les différents prototypes

#### Les fleurs
| Prototype 1                                                                                      | Prototype 2                                                                                      | Prototype 03                                                                                     | Fleur finale                                                                                         |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| ![prototype_01](https://github.com/user-attachments/assets/747c9423-8ccd-490e-b17e-11212664e013) | ![prototype_02](https://github.com/user-attachments/assets/52870faf-2a4a-47f2-b50a-ef6d72d4afe2) | ![prototype_03](https://github.com/user-attachments/assets/19c9f100-eebc-4046-94e3-1ea79bf9bea3) | ![prototype_finale](https://github.com/user-attachments/assets/138edf2f-8060-4c23-8c96-91cf7e2427ce) |

#### La plaque métallique
| Prototype 1                                                                                      | Prototype 2                                                                                      | Prototype 3                                                                                      | Plaque finale                                                                                        |
| ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| ![prototype_01](https://github.com/user-attachments/assets/a8e3cfb5-b7d5-4784-a9e2-f3bf43485bbe) | ![prototype_02](https://github.com/user-attachments/assets/5a681163-cc7e-4ab2-845d-6b757697a32a) | ![prototype_03](https://github.com/user-attachments/assets/a6e8fe81-631c-4c1a-8f09-09745df01d09) | ![prototype_finale](https://github.com/user-attachments/assets/01d67a14-95b7-462a-8dd1-4e5ccd30baf9) |

## Fonctionnement
### Flux de données et d’interactions
À la base de la maquette, Arduino acquiert les différentes valeurs de la capacitance et les transmet à Puredata. Dans Puredata, les données brutes de la capacitance ainsi qu'un booléen 1/0 permettant d'identifier le moment de l'interaction sont utilisés et modifiés. Ces deux données permettent d'affecter l'éclairage des fleurs, l'audio et les deux projections. Celles-ci sont ensuite acheminées à Reaper, Qlc+ et TouchDesigner par l'attribution de ports spécifiques.

#### Reaper  
Les données booléennes de PureData sont envoyées à Reaper, qui les utilise pour déclencher trois sons en fonction de l'interaction avec la plaque. Lorsque l’utilisateur pose sa main sur la plaque, un son magique est joué, suivi d’un son de ruissellement d’eau tant que le contact est maintenu. Dès que la main est retirée, un son de grenouille se fait entendre, signalant la fin de l’interaction sonore.  

#### QLC+  
En parallèle, ces mêmes données booléennes sont envoyées à QLC+ pour déclencher un chaser lumineux.  
Lorsque l’utilisateur interagit avec la plaque, le chaser s’active et illumine les ampoules avec des teintes de rose, créant une ambiance visuelle synchronisée avec le son.  

#### TouchDesigner  
Enfin, les données brutes sont transmises à TouchDesigner pour modifier la projection visuelle.  
Lorsque l’utilisateur pose sa main sur la plaque, le visuel s’intensifie, renforçant l’immersion dans l'expérience interactive.  
À l’inverse, lorsque la main est retirée, les effets visuels s’atténuent progressivement, accompagnant la fin du son et des lumières.  

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
    Reaper-->| Plaque active |DéclenchementSonCourt1[Déclenchement du premier son court];
    DéclenchementSonCourt1-->| Délai de 7 secondes |DéclenchementSonLong[Déclenchement du son long]
    Reaper-->| Plaque inactive |DéclenchementSonCourt2[Déclenchement du deuxième son court];
    TouchDesignerSol-->| Plaque inactive |AtténuationVisuel[Atténuation du visuel];
    TouchDesignerSol-->| Plaque active |IntensificationVisuel[Intensification du visuel];
    TouchDesignerMur-->| Plaque inactive |AtténuationVisuel[Atténuation du visuel];
    TouchDesignerMur-->| Plaque active |IntensificationVisuel[Intensification du visuel];
```

### Synoptique
```mermaid
flowchart TD
    subgraph Plafond
        A[Alimentation] --> B[Projecteur du sol 192.168.1.180]
        A --> C[Ampoule 1]
        A --> D[Ampoule 2]
        A --> E[Ampoule 3]
        A --> F[HDMI Extender RX #31]
        F -->| Cable HDMI | B
        G[Ethernet Port 94] -->| Cable Ethernet | B
        H[Ethernet Port 93] -->| Cable Ethernet | F
        A --> I[Projecteur du mur 192.168.1.21]
        K[Ethernet Port 81] -->| Cable Ethernet | I
        L[Ethernet Port 80] -->| Cable Ethernet | M[HDMI Extender RX #15]
        M --> I
        A --> M
    end
```
```mermaid
flowchart TD
    subgraph Sol
        N[Alimentation] --> O
        O[HDMI Extender TX #31] -->| Cable HDMI | P[Ordinateur 192.168.1.178]
        Q[Ethernet Port 247] -->| Cable Ethernet | O
        N --> R[Speaker]
        R -->| Cable XLR | S[Adaptateur Audio]
        N --> T
        T[Carte de son] --> U[Ordinateur 192.168.1.150]
        N --> V
        V[TP Link] --> | Ethernet Port 219 | Atom
        Atom --> | Tape d'aluminum | X[Plaque en acier]
        Y[ Ethernet Port 253] --> Atom
        V --> | Ethernet Port 218 | Ethernet
        V --> | Cable Ethernet | W[Ordinateur 192.168.1.140]
    end
```
```mermaid
flowchart TD
    subgraph Sol audio
        N[Alimentation] --> O
        O[ plaque 1 speaker] -->| cable XLR | P[port 168] -->| cable XLR | H[ port 145]
        N --> R[Plaque 2 speaker]
        R -->| Cable XLR | S[port 166] -->| cable XLR | I[ port 146]
        N --> T
        T[Plaque speaker 3] -->| cable XLR | U[ port 165] -->| cable XLR | G[ port 147]
        G -->| cable XLR | F
        I -->| cable XLR | F
        H -->| cable XLR | F
        F[Carte de son] --> W[Ordinateur 192.168.1.150]
    end
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
* ![plaque_01](https://github.com/user-attachments/assets/dfe778a3-c84e-4ea5-a6f4-d594e4b90af6)
* ![support](https://github.com/user-attachments/assets/cb75d7d5-3a9a-4152-86ad-d07a3197a7ff)
* ![ordinateur_01](https://github.com/user-attachments/assets/7516ee77-bdca-49d4-8ab3-8375a490665b)
* ![ordinateur_02](https://github.com/user-attachments/assets/0b09c854-46ff-40fd-b184-261d9ca66335)
* ![structure_base](https://github.com/user-attachments/assets/dc4a95c4-583d-454c-aac3-53559fe59865)
* ![projection](https://github.com/user-attachments/assets/46979407-bc4a-4576-be79-92e1c6e9e297)

## Vidéo du la maquette en action

<iframe width="560" height="315" src="https://www.youtube.com/embed/9Ty8B9qVx1c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/_t8blyjZfRY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
