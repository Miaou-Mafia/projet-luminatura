# Diffusion

## Gallerie d'images
* ![aucune-interaction](https://github.com/user-attachments/assets/306fa42f-b9b6-4596-8120-fabcc7c78eef)
* ![plaque-01](https://github.com/user-attachments/assets/9bce0a48-83cb-40df-86f6-1ac358bd8311)
* ![plaque-02](https://github.com/user-attachments/assets/ce9d6fa1-c6c3-4f0b-b6cb-2bc4536e9d16)
* ![plaque-03](https://github.com/user-attachments/assets/3c2421e2-7da4-4272-a792-2fe263778f39)
* ![plaques-01-03](https://github.com/user-attachments/assets/29f1d428-2cfd-4421-8487-ebd94aecb473)
* ![plaques-02-03](https://github.com/user-attachments/assets/65b8cebd-30ef-47da-816a-c687abae156e)
* ![plaques-01-02](https://github.com/user-attachments/assets/6041456b-24b0-420a-b762-fe2dfe2dbfc1)
* ![plaques-01-02-03](https://github.com/user-attachments/assets/195386a9-fa41-4988-9b5d-e6a0a3d046fa)
* ![support-plaques](https://github.com/user-attachments/assets/e5e5e17f-3baa-46a1-bcaf-bcc17b8d78df)

## Documentation vidéo

<iframe width="560" height="315" src="https://www.youtube.com/embed/Jz4wxeXT_2w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## Documentation vidéo de l'installation en action

## Manuel d'instruction pour opération

### Gestion des logiciels sur deux ordinateurs

Ordinateur 1 (PC):
* QLC+
* Reaper avec Plugdata
* TouchDesigner (Projection au mur)

Ordinateur 2 (Ordinateur portable):
* Arduino
* Pure Data
* Touch Designer (Projection au sol)
  
## Salle des matrice (caché des utilisateurs)

<img src="https://github.com/user-attachments/assets/2f296e52-1c35-4567-95b5-e5c6ea34a18c" width="400" height="400">
<img src="https://github.com/user-attachments/assets/15218715-8b0d-4126-994e-1c94d3b51495" width="400" height="400">
<img src="https://github.com/user-attachments/assets/79d05f63-8f49-4007-8c4b-2457cd7f434d" width="400" height="400">
<img src="https://github.com/user-attachments/assets/503f4bb1-4e80-4a42-a90e-9143ae625447" width="400" height="400">
<img src="https://github.com/user-attachments/assets/72ee30ba-3589-4563-8c48-b725dce71819" width="400" height="400">
<img src="https://github.com/user-attachments/assets/5f55a309-024c-4d32-916e-9d68ca214d37" width="400" height="400">
<img src="https://github.com/user-attachments/assets/5e6cebc1-6b58-4f26-86ed-9d3bcf7911a7" width="400" height="400">


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
    Donne1-0-->| Port: 10003,10005,10007,10008,10009,10010 |Reaper;
    QLC+-->ActivationChaser[Activation du chaser rose par l'intensité lumineuse];
    Reaper-->| Plaque active |DéclenchementSonCourt1[Déclenchement du premier son court];
    DéclenchementSonCourt1-->| Délai de 7 secondes |DéclenchementSonLong[Déclenchement du son long]
    Reaper-->| Plaque inactive |DéclenchementSonCourt2[Déclenchement du deuxième son court];
    TouchDesignerSol-->| Plaque inactive |AtténuationVisuel[Atténuation du visuel];
    TouchDesignerSol-->| Plaque active |IntensificationVisuel[Intensification du visuel];
    TouchDesignerMur-->| Plaque inactive |AtténuationVisuel[Atténuation du visuel];
    TouchDesignerMur-->| Plaque active |IntensificationVisuel[Intensification du visuel];
```

### Les différents ports utilisés
| Port  | Fonction                                        |
| ----- | ----------------------------------------------- |
| 8001  | Atom M5 Stack 1                                 |
| 8002  | Atom M5 Stack 2                                 |
| 8003  | Atom M5 Stack 3                                 |
| 10001 | QLC+                                            |
| 10002 | TouchDesigner - projection au sol               |
| 10003 | Reaper avec le premier patch sur Plugdata       |
| 10004 | TouchDesigner - projection sur le mur           |
| 10005 | Reaper avec le deuxième patch sur Plugdata      |
| 10007 | Reaper avec le troisième patch sur Plugdata     |
| 10008 | Reaper avec les données des plaques 01 (climax) sur Plugdata     |
| 10009 | Reaper avec les données des plaques 02 (climax)  sur Plugdata     |
| 10010 | Reaper avec les données des plaques 03 (climax) le troisième patch sur Plugdata     |

### Audio 

| Haut-parleurs      | Carte de son (sortie) |
| ------------------ | --------------------- |
| Genelec plaque 01  | 05                    |
| Genelec plaque 02  | 06                    |
| Genelec plaque 03  | 03                    |

```mermaid
flowchart TD
    subgraph Câblage pour l'audio
        N[Alimentation] --> O
        O[ Genelec plaque 01 ] -->| Cable XLR | P[port 168] -->| Cable XLR | H[ port 145]
        N --> R[Genelec plaque 03 ]
        R -->| Cable XLR | S[port 166] -->| cable XLR | I[ port 146]
        N --> T
        T[Genelec plaque 02 ] -->| Cable XLR | U[ port 165] -->| Cable XLR | G[ port 147]
        G -->| Cable XLR | F
        I -->| Cable XLR | F
        H -->| Cable XLR | F
        F[Carte de son Behringer] --> W[Ordinateur 192.168.1.150]
    end
```
#### Reaper

Effets sonores pour la plaque 1
* Magie
* Ruisseau
* Sons aléatoire début
  * Bambo
  * Echo
  * GardenChime
  * Pad méditation
* Sons aléatoire fin
  * Grenouille-01
  * Cloche
  * Hibou

Effets sonores pour la plaque 2
* Tambour
* Méditation
* Sons aléatoire début
  * Flute
  * Flute célestiale
  * Flute célestiale 2
  * UpLifting 2
* Sons aléatoire fin
  * Vent
  * Feuilles
  * Grenouille-01

Effets sonores pour la plaque 3
* Magie 02
* Oiseaux
* Sons aléatoire début
    * Echo
    * Pad méditation
    * UpLifting
    * GardenChime
* Sons aléatoire fin
    * Grenouille-01
    * Libellule
    * Grenouille-02

#### Configuration de base de Reaper

![reaper-configuration](https://github.com/user-attachments/assets/80f0c5c9-ae88-4906-af13-48b35c6f176d)
![reaper-preference-audio](https://github.com/user-attachments/assets/2ab5222d-3481-4ff8-b7e8-89830931cd9d)

#### Ambiance 

![ambiance-route](https://github.com/user-attachments/assets/e8c4265e-c8be-4f7b-8650-8ca624110938)
![ambiance-route-fx](https://github.com/user-attachments/assets/45d0068b-ae44-4a5b-a136-bc7fb26a67a6)

#### Ambiance Stéreo

![ambiance-route](https://github.com/user-attachments/assets/cccc0c93-1158-4209-9622-c0e584b44363)
![ambiance-fx](https://github.com/user-attachments/assets/47ec3c3f-fef5-4511-a040-b31eff86264c)

#### Plaque 1

![plaque-01](https://github.com/user-attachments/assets/6701c1ea-6215-4f23-a1f8-b06cb6102540)

#### Plaque 2

![plaque-02](https://github.com/user-attachments/assets/58c4664b-9f09-4b66-bdac-abbfaf259a3e)

#### Plaque 3

![plaque-03](https://github.com/user-attachments/assets/090340df-f336-4132-acf6-9aa93d4efbbb)

#### Compression 

![bus-compresseur](https://github.com/user-attachments/assets/d81f4b41-8700-4813-8728-8307eb4c3970)

#### Master

![master-route](https://github.com/user-attachments/assets/9d82261e-3d2e-4373-a4be-2a5e41ac3f93)
![master-fx](https://github.com/user-attachments/assets/1bea3d62-1ef9-4e70-a273-0d391dc1e446)

#### Plug Data

Plaque 1

| Sons     | Note midi |
| -------- | --------- |
| Magie | 60  |
| Ruisseau | 62  |
| Grenouille-01 | 64  |
| Cloche | 65   |
| Hibou | 67  |
| Bambo | 84  |
| Echo | 86  |
| GardenChime | 88   |
| Pad méditation |89  |

Plaque 2

| Sons     | Note midi |
| -------- | --------- |
| Tambour | 60  |
| Méditation | 62  |
| Grenouille-01 | 64  |
| Feuilles | 65   |
| Vent | 67  |
| Flute | 91  |
| Flute-célestiale | 92  |
| Flute célestiale 02 | 94   |
| UpLifting 02 | 95  |

Plaque 3

| Sons     | Note midi |
| -------- | --------- |
| Magie-02 | 60  |
| Oiseaux | 62  |
| Grenouille-02 | 64  |
| Libellule | 65   |
| Grenouille-01 | 67  |
| Echo | 88  |
| Pad meditation | 86  |
| UpLifting | 89   |
| GardenChime | 91  |

Gouttes d'eau pour les 3 plaques

| Sons     | Note midi |
| -------- | --------- |
| Goutte-03 | 72  |
| Goutte-04 | 74  |
| Goutte-05 | 76  |
| Goutte-06 | 77   |

### Lumières

**Association des lumières**

## Associer les lumières une à une

- Un canal par lumière.

1. Choisir un canal spécifique et allumer la lumière. Dans les 10 secondes suivantes, cliquer trois fois sur le bouton "set" du transmetteur. La lumière devrait clignoter trois fois en vert pour indiquer son association.

2. Pour associer une deuxième lumière :
   - Éteindre la première lumière déjà associée.
   - Changer de canal sur le transmetteur.
   - Allumer la deuxième lumière et répéter le même processus que pour la première lumière.

## Dissociation des lumières

1. Éteindre les lumières et les rallumer.
2. Dans les 5 secondes suivantes, appuyer cinq fois sur le bouton "set" du transmetteur. Les lumières devraient clignoter dix fois en rouge pour indiquer leur dissociation du transmetteur.


| Ampoules    | Canaux   |
| ----------- | -------- |
| Ampoule 01  | Canal 01 |
| Ampoule 02  | Canal 02 |
| Ampoule 03  | Canal 03 |
| Ampoule 04  | Canal 04 |
| Ampoule 05  | Canal 05 |
| Ampoule 06  | Canal 06 |

#### QLC+

| Universe   | Lumières              | USB DMX |
| ---------- | --------------------- | ------- |
| Universe 1 | Ampoule DMX 512 RGB   | DMX Output 1 - (S/N 6A009218)    |
| Universe 2 | Lumière generic dimer | DMX Output 1 - (S/N 6A009219)  |

Universe 1

| Lumière        | Adresse    |
| -------------- | ---------- |
| Generic RGBW 1 | 001 - 005  |
| Generic RGBW 2 | 006 - 0010 |
| Generic RGBW 3 | 011 - 015  |
| Generic RGBW 4 | 016 - 020  |
| Generic RGBW 5 | 021 - 025  |
| Generic RGBW 6 | 026 - 030  |

Universe 2

| Lumière   | Adresse |
| --------- | ------- |
| Dimmers 1 | 001     |
| Dimmers 2 | 002     |
| Dimmers 3 | 003     |

Virtual Console

| Slider | Input channel |
| ------ | ------------- |
| Rose   | 1957          |
| Bleu   | 64162         |
| Jaune  | 21930         |
| Vert   | 7907          |
| Mauve  | 15909         |
| Rouge  | 49812         |
| Climax | 45760         |
| Light 1 | 48632       |
| Light 2  | 36717       |
| Light 3 | 40678        |

### Visuel

#### Câblage des projections
![cable-01](https://github.com/user-attachments/assets/7fcb55c2-e76b-4ce1-8695-3b5d89a4dd4f)
![cable-02](https://github.com/user-attachments/assets/d37ef38d-fccf-4624-9946-1a74f2750046)
![cable-03](https://github.com/user-attachments/assets/2fa6806d-27e9-476f-b003-168e08abbf41)
![cable-04](https://github.com/user-attachments/assets/2aa57611-7299-45b1-8a8d-909bb80f4b5b)
![cable-05](https://github.com/user-attachments/assets/50c1d5c5-97e4-4a0b-a524-e1c7e152a79b)
![cable-06](https://github.com/user-attachments/assets/88e2eb11-c6f1-4c22-b0a9-f3f30238ffc3)
![cable-07](https://github.com/user-attachments/assets/5fb9b882-5602-46ef-a645-7a1251d811cb)
![cable-08](https://github.com/user-attachments/assets/0e24b962-1b99-4c92-a913-2cc3ea66616d)

```mermaid
flowchart TD
subgraph Plafond
    A[Alimentation] --> B[Projecteur du sol 192.168.1.180]
    A --> C[Ampoule 1]
    A --> D[Ampoule 2]
    A --> E[Ampoule 3]
    A --> X[Ampoule 4]
    A --> Y[Ampoule 5]
    A --> Z[Ampoule 6]
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
#### TouchDesigner

## Effets visuels pour toutes les plaques

### Projection du mur
- Deux des 6 particules GPU passent de 10 particules à 500 quand l'une des plaques est touchée.
- Le gamma devient de plus en plus fort quand la surface des mains augmente.
- Toutes les particules GPU passent au mauve quand la plaque 1 et la plaque 2 sont activées.
- Toutes les particules GPU passent au vert quand la plaque 2 et la plaque 3 sont activées.
- Toutes les particules GPU passent au rouge quand la plaque 1 et la plaque 3 sont activées.
- Toutes les particules GPU changent de couleur (mauve, vert, rouge, rose, bleu, jaune) par intervalle quand toutes les plaques sont activées.
- Quand toutes les plaques sont activées, le vent des particules GPU se met en mouvement grâce à des LFOs.

# Effets visuels pour la plaque 1

## Projection du sol
- Les particules GPU passent d'une force qui se concentre au centre à une force qui se concentre vers la plaque 1 (centre).

## Projection du mur
- Toutes les particules GPU passent au rose quand la plaque 1 est activée.

# Effets visuels pour la plaque 2

## Projection du sol
- Les particules GPU passent d'une force qui se concentre au centre à une force qui se concentre vers la plaque 2 (gauche).

## Projection du mur
- Toutes les particules GPU passent au bleu quand la plaque 2 est activée.

# Effets visuels pour la plaque 3

## Projection du sol
- Les particules GPU passent d'une force qui se concentre au centre à une force qui se concentre vers la plaque 3 (droite).

## Projection du mur
- Toutes les particules GPU passent au jaune quand la plaque 3 est activée.

### Interactivité

#### Arduino


| Port | Fonction        | ID  |
| ---- | --------------- | --- |
| 8001 | Atom M5 Stack 1 | 01  |
| 8002 | Atom M5 Stack 2 | 02  |
| 8003 | Atom M5 Stack 3 | 03  |


#### Pure Data

```mermaid
graph TD;  

    Plaque_01 -->| Reaper| alpha;
    Plaque_01 -->| Reaper| beta;
    Plaque_01 -->| Touch designer | omega1;
    Plaque_01 -->| Touch Designer | qlc1;
```
```mermaid
graph TD;  
    Plaque_02 -->| Reaper| alpha;
    Plaque_02 -->| Reaper| beta;
    Plaque_02 -->| Touch designer | omega2;
    Plaque_02 -->| Touch Designer | qlc2;
```
```mermaid
graph TD;  
    Plaque_03 -->| Reaper | alpha;
    Plaque_03 -->| Reaper| beta;
    Plaque_03 -->| Touch designer | omega3;
    Plaque_03 -->| Touch designer | qlc3;
```
