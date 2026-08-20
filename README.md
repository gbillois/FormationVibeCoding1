# FormationVibeCoding1

Mini-jeu Snake autonome pour valider des connaissances en cybersécurité. Ouvrez
`index.html` dans un navigateur moderne pour jouer ; aucune dépendance ni étape
de compilation n'est nécessaire.

## Audit du code

Audit réalisé le 20 août 2026 sur l'application statique :

- **Corrigé — affichage du plateau :** la hauteur interne du canvas ne
  correspondait pas aux 16 lignes de 30 pixels. La dernière ligne pouvait donc
  être tronquée. Le canvas et son ratio CSS utilisent maintenant 720 × 480.
- **Corrigé — demi-tour rapide :** plusieurs touches saisies entre deux cycles
  pouvaient autoriser un demi-tour du serpent. La prochaine direction est
  désormais comparée à la dernière direction mise en file.
- **Corrigé — mélange des questions :** le tri avec un comparateur aléatoire
  n'assurait pas un mélange uniforme. Il est remplacé par Fisher-Yates.
- **Corrigé — construction des réponses :** les réponses sont créées avec les
  API DOM et `textContent`, plutôt qu'avec `innerHTML`. Cela évite qu'une future
  banque de questions externe introduise du balisage non fiable.
- **Corrigé — accessibilité :** le canvas, les commandes tactiles et la boîte de
  résultat ont des libellés explicites, les boutons ont un focus visible et le
  bouton de rejeu reçoit le focus à la fin d'une partie.

## Recommandations restantes

1. Séparer HTML, CSS, logique de jeu et banque de questions en fichiers dédiés
   si l'application continue à évoluer.
2. Ajouter des tests automatisés de la logique pure (collisions, directions,
   score et sélection des questions) après cette séparation.
3. Ajouter un piège à focus complet dans les boîtes de dialogue pour une prise
   en charge clavier plus stricte.
4. Définir une politique CSP au niveau du serveur lors du déploiement. Le style
   et le script intégrés devront alors être externalisés afin d'éviter
   `unsafe-inline`.
