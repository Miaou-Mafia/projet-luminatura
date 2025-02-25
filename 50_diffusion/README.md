# Diffusion
## Description

## Gallerie d'images
* ![Image 1](https://placehold.co/400x400?text=1+image)
* ![Image 2](https://placehold.co/400x400?text=2+image)
* ![Image 3](https://placehold.co/400x400?text=3+image)
* ![Image 4](https://placehold.co/400x400?text=4+image)

## Fonctionnement

### Flux de données et d’interactions

#### Reaper

#### QLC+

#### TouchDesigner

### Synoptique

```mermaid
flowchart TD
    subgraph Câblage pour l'audio
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

## Logiciels et Scripts

## Gestion des données et des logiciels

### Gestion des logiciels sur deux ordinateurs

### Les différents ports utilisés
| Port  | Fonction                              |
| ----- | ------------------------------------- |
| 10001 | Qlc+                                  |
| 10002 | TouchDesigner - projection sur le sol |
| 10003 | Reaper incluant le premier patch sur Plugdata   |
| 10004 | TouchDesigner - projection sur le mur |
| 10005 | Reaper incluant le deuxième patch sur Plugdata   |
| 10007 | Reaper incluant le troisième patch sur Plugdata   |
