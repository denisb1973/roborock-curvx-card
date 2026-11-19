# Roborock Qrevo CurvX — Dashboard personnalisé

Carte Lovelace indépendante pour Home Assistant : onglets **Accueil, Carte, Historique, Station, Entretien et Réglages**, présentés dans un style sombre inspiré du tableau de bord du poêle à granulés.

## Installation depuis HACS / Marketplace

1. Dans Home Assistant, ouvrir **HACS / Marketplace** puis **Dépôts personnalisés**.
2. Ajouter : `https://github.com/denisb1973/roborock-curvx-card`.
3. Sélectionner la catégorie **Tableau de bord / Dashboard (plugin)** et installer la carte.
4. Si la ressource n'a pas été ajoutée automatiquement, ajouter dans **Paramètres → Tableaux de bord → Ressources** :
   - URL : `/hacsfiles/roborock-curvx-card/roborock-curvx-card.js`
   - Type : **Module JavaScript**
5. Sur un tableau de bord, ajouter une carte **Manuelle** :

```yaml
type: custom:roborock-curvx-card
background: /local/roborock/roborock_salon.png
```

## Photo de fond

La photo de salon n'est pas encore distribuée par le dépôt. Déposer `roborock_salon.png` dans `/config/www/roborock/`. Sans l'image, la carte affiche un fond uni. Ne pas ajouter de texte ni de boutons sur l'image : ils sont produits par le composant et restent interactifs.

## Entités

Le composant utilise par défaut :
- `vacuum.salle_a_manger_roborock_qrevo_curvx`
- `image.salle_a_manger_roborock_qrevo_curvx_map_0`
- les capteurs, listes et interrupteurs préfixés par `salle_a_manger_roborock_qrevo_curvx`.

Pour remplacer robot et carte :

```yaml
type: custom:roborock-curvx-card
vacuum: vacuum.salle_a_manger_roborock_qrevo_curvx
map: image.salle_a_manger_roborock_qrevo_curvx_map_0
background: /local/roborock/roborock_salon.png
```

## Fonctionnement

Les commandes Démarrer, Pause et Retour à la base utilisent les services Home Assistant. Dans les onglets Réglages et Station, les sélecteurs et interrupteurs appellent les services correspondants. **Le vidage, le séchage et le lavage déclenchent de vraies opérations** : à lancer uniquement lorsque les conditions sont réunies.

La carte du logement utilise l'image publiée par l'intégration Roborock. **La sélection tactile des pièces n'est pas implémentée** et le suivi du robot en mouvement doit être confirmé pendant un nettoyage réel.

## État du développement

Version initiale **0.1.0**. Les fichiers sont désormais dans un dépôt distinct de celui du poêle. Aucune GitHub Action n'est nécessaire pour ajouter la carte en tant que dépôt personnalisé. Les fichiers ont été ajoutés sur GitHub, mais **l'installation et le rendu dans ton Home Assistant restent à tester**.
