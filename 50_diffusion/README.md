# Diffusion

## Gallerie d'images
* ![Image 1](https://placehold.co/400x400?text=1+image)
* ![Image 2](https://placehold.co/400x400?text=2+image)
* ![Image 3](https://placehold.co/400x400?text=3+image)
* ![Image 4](https://placehold.co/400x400?text=4+image)

## Vidéo

## Documentation vidéo de l'installation en action

## Manuel d'instruction pour opération

### Gestion des logiciels sur deux ordinateurs

Ordinateur 1 (PC):
* QLC+
* Reaper avec Plugdata
* Touch Designer (Projection au mur)

Ordinateur 2 (Ordinateur portable):
* Arduino
* Puredata
* Touch Designer (Projection au sol)

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

### Les différents ports utilisés
| Port  | Fonction                                        |
| ----- | ----------------------------------------------- |
| 8001  | Atom M5 Stack 1                                 |
| 8002  | Atom M5 Stack 2                                 |
| 8003  | Atom M5 Stack 3                                 |
| 10001 | Qlc+                                            |
| 10002 | TouchDesigner - projection sur le sol           |
| 10003 | Reaper incluant le premier patch sur Plugdata   |
| 10004 | TouchDesigner - projection sur le mur           |
| 10005 | Reaper incluant le deuxième patch sur Plugdata  |
| 10007 | Reaper incluant le troisième patch sur Plugdata |

### Audio 

| Haut-parleurs     | Carte de son (sortie) |
| ----------------- | --------------------- |
| Genelec plaque 01 | 05                    |
| Genelec plaque 02 | 06                    |
| Genelec plaque 03 | 03                    |

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
* Sons aléatoire
  * Grenouille-01
  * Cloche
  * Hibou

Effets sonores pour la plaque 2
* Tambour
* Méditation
* Sons aléatoire
  * Vent
  * Feuilles
  * Grenouille-01

Effets sonores pour la plaque 3
* Magie 02
* Oiseaux
* Sons aléatoire
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

Plaque 2

| Sons     | Note midi |
| -------- | --------- |
| Tambour | 60  |
| Méditation | 62  |
| Grenouille-01 | 64  |
| Feuilles | 65   |
| Vent | 67  |

Plaque 3

| Sons     | Note midi |
| -------- | --------- |
| Magie-02 | 60  |
| Oiseaux | 62  |
| Grenouille-02 | 64  |
| Libellule | 65   |
| Grenouille-01 | 67  |

Gouttes d'eau pour les 3 plaques

| Sons     | Note midi |
| -------- | --------- |
| Goutte-03 | 72  |
| Goutte-04 | 74  |
| Goutte-05 | 76  |
| Goutte-06 | 77   |

### Lumières

**Association des lumières**

*Associer les lumières une à la fois

*Un channel par lumière

Choisir un channel spécifique et allumer la lumière. Dans les 10 prochaines secondes, cliquer trois fois sur le bouton set du transmetteur. La lumière devrait clignoter 3 fois en vert pour démontrer son association.

Pour une seconde lumière, éteindre la première lumière déjà associée et changer de channel sur le transmetteur. Maintenant, allumer la deuxième lumière et refaire le même processus que fait précédemment sur la première lumière.

**Disassociation des lumières**

Éteindre les lumières et les rallumer. Dans les 5 prochaines secondes, appuyer 5 fois sur le bouton set du transmetteur. Les lumières devraient clignoter 10 fois en rouge pour démontrer leur dissociation du transmetteur.

| Ampoules   | Canal    |
| ---------- | -------- |
| Ampoule 01 | Canal 01 |
| Ampoule 02 | Canal 02 |
| Ampoule 03 | Canal 03 |
| Ampoule 04 | Canal 04 |
| Ampoule 05 | Canal 05 |
| Ampoule 06 | Canal 06 |

#### QLC+

| Universe   | Lumières              | USB DMX |
| ---------- | --------------------- | ------- |
| Universe 1 | Ampoule DMX 512 RGB   |  DMX Output 1 - (S/N 6A009218)    |
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

#### TouchDesigner

Effets visuels pour toutes les plaques
* Projection du mur
    * Deux des 6 particles GPU passent de 10 particules à 500 quand une des plaques est touchée.
    * Le gamma devient de plus en plus fort quand les surfaces des mains augmentent
    * Toutes les particles GPU passent au mauve quand la plaque 1 et la plaque 2 sont activées
    * Toutes les particles GPU passent au vert quand la plaque 2 et la plaque 3 sont activées
    * Toutes les particles GPU passent au rouge quand la plaque 1 et la plaque 3 sont activées
    * Toutes les particles GPU changent de couleur (mauve, vert, rouge, rose, bleu, jaune) en interval quand toutes les plaques sont activées
    * Quand toutes les plaques sont activées, le vent du particles GPU se mets en mouvement grâce à des LFOs

Effets visuels pour la plaque 1
* Projection du sol
    * Le particles GPU passe d'une force qui se focus au centre à une force qui se focus vers la plaque 1 (centre)
      
* Projection du mur
    * Toutes les particles GPU passent au rose quand la plaque 1 est activée

Effets visuels pour la plaque 2
* Projection du sol
    * Le particles GPU passe d'une force qui se focus au centre à une force qui se focus vers la plaque 2 (gauche)
      
* Projection du mur
    * Toutes les particles GPU passent au bleu quand la plaque 2 est activée

Effets visuels pour la plaque 3
* Projection du sol
    * Le particles GPU passe d'une force qui se focus au centre à une force qui se focus vers la plaque 3 (droite)

* Projection du mur
    * Toutes les particles GPU passent au jaune quand la plaque 3 est activée

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
