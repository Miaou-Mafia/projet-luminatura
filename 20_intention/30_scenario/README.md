# Scénario

## Scénario interractif
```mermaid
graph TD;
    ModeVeille[Mode veille] --> AmbianceBase[Lumière et audio de base jouent];
    AmbianceBase --> Interaction[Interaction avec une plaque ?];
    
    Interaction -- Oui --> Plaque1[Utilisateur touche la plaque];
    Plaque1 --> Capteur1[Capteur de capacitance activé];
    
    Capteur1 --> Lumière1[Lumière modifiée pour l'utilisateur];
    Capteur1 --> Audio1[Audio modifié pour l'utilisateur];
    
    Lumière1 --> Reste1[Utilisateur reste ?];
    Audio1 --> Reste1;
    
    Reste1 -- Oui --> PlusEffetsLumière1[Effets lumières augmentés];
    Reste1 -- Oui --> PlusEffetsAudio1[Effets audio augmentés];
    Reste1 -- Non --> RetourVeille[Retour au mode veille];
    
    Interaction -- Non --> AmbianceBase;

```

## Expérience usager UX
...

<!-- Ici mettre tous les documents et références concernant la scéanrisation de l'expérience   -->

* Tous les verbes disponibles à vos interacteurs

* Tous les objets sur lesquels chaque verbe peut agir et comment ils le font

* Actions émergentes que vous aimeriez que vos interacteurs effectuent

* Toutes les façons que les interacteurs peuvent faire progresser l’expérience

<!--- 
## Références

* [Scénario Interactif](https://tim-montmorency.com/582523-gestion/#/contenus/2_scenarisation/20_scenario/20_interactif/)
* [Expérience usager UX](https://tim-montmorency.com/582523-gestion/#/contenus/2_scenarisation/20_scenario/40_ux/)
---> 

