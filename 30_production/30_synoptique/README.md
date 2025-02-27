# Synoptique

```mermaid
graph TD;  
  %% Composants     
  Ordinateur["Contrôle principal - Ordinateur 1"] 
  Ordinateur-Portable["Contrôle secondaire - Ordinateur 2"]  
  DMX["USB DMX"]     
  Lumieres["Lumières"]     
  Ampoule["Ampoules"]     
  CarteSon["Carte de son"]     
  HautParleur["Haut-parleurs"]     
  SortieAudio["Sortie audio"]      
  PlaqueMetalique["Plaques métalliques"]     
  Arduino["Arduino M5 Stack"]     
  Projecteur1["Projecteur 1"]   
  Projecteur2["Projecteur 2"]   
  
  %% Emplacements     
  subgraph Caché_des_utilisateurs         
    Ordinateur     
    Ordinateur-Portable
  end     
  subgraph Plafond         
    DMX         
    Lumieres         
    Ampoule     
  end     
  subgraph Grand_Studio         
    PlaqueMetalique         
    Arduino     
    Projecteur1  
    Projecteur2  
    CarteSon
    HautParleur
    SortieAudio
  end     
  
  %% Connexions     
  Ordinateur --> DMX     
  Ordinateur --> CarteSon     
  Ordinateur -.-> PlaqueMetalique     
  Ordinateur-Portable --> PlaqueMetalique
  PlaqueMetalique --> Arduino     
  Arduino -->|Contrôle Lumière| Lumieres     
  Arduino -->|Contrôle Son| CarteSon     
  Arduino -->|Contrôle Visuel| Projecteur1 
  Arduino -->|Contrôle Visuel| Projecteur2
  DMX -->|Câble DMX| Lumieres     
  Lumieres -->|Câble électrique| Ampoule     
  CarteSon -->|Câble audio| HautParleur     
  HautParleur -->|Câble audio| SortieAudio  
  Projecteur1 -->|Câble Vidéo| Ordinateur
  Projecteur2 -->|Câble Vidéo| Ordinateur-Portable

```
