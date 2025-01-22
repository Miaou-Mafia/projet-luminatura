# Synoptique
```mermaid
graph TD;

%% Composants
    Ordinateur[Contrôle central - Ordinateur]
    DMX[USB DMX]
    Lumieres[Lumières]
    Ampoule[Ampoules]
    CarteSon[Carte de son]
    HautParleur[Haut-parleurs]
    SortieAudio[Sortie audio]

    PlaqueMetalique[Plaque métallique]
    ArduinoA000066[Arduino A000066]

    %% Emplacements
    subgraph Caché des utilisateurs
        Ordinateur
    end

    subgraph Plafond
        DMX
        Lumieres
        Ampoule 
        CarteSon
        HautParleur
        SortieAudio
    end

    subgraph Grand Studio
        PlaqueMetalique
        ArduinoA000066
    end

    %% Connexions
    Ordinateur -->|USB| DMX
    Ordinateur --> CarteSon
    Ordinateur -.-> PlaqueMetalique
    PlaqueMetalique -->|Capteur de capacitance Adafruit Industries LLC 1374| ArduinoA000066
    ArduinoA000066 -->|Contrôle Lumière| Lumieres
    ArduinoA000066 -->|Contrôle Son| CarteSon
    DMX -->|Câble DMX| Lumieres
    Lumieres -->|Câble électrique| Ampoule
    CarteSon -->|Câble audio| HautParleur
    HautParleur -->|Câble audio| SortieAudio

```
<!--- 
## Références

* [Synoptique](https://tim-montmorency.com/582523-gestion/#/contenus/3_planification/10_synoptique/)
--->

