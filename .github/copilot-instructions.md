# Règles de publication des logs

- Traite un message comme une commande de publication uniquement s'il commence exactement par `/log ` (la commande est sensible à la casse et doit être suivie d'une espace).
- Pour une telle commande, récupère tout le texte après le préfixe `/log `, sans ajouter le préfixe au contenu publié et sans tronquer le texte. Ajoute une entrée à `logs.json` contenant le message et la date/heure réelle de publication.
- Génère la date et l'heure à partir de l'horloge réelle au moment du traitement, dans le fuseau `Europe/Paris`. Enregistre la date comme chaîne ISO 8601 avec son décalage horaire explicite (`+01:00` ou `+02:00`, selon la date). N'invente jamais une heure si l'horloge réelle n'est pas disponible.
- `logs.json` est un tableau JSON. Ajoute la nouvelle entrée en conservant toutes les entrées existantes; ne remplace ni ne supprime jamais les anciens logs. Chaque entrée a la forme `{"message":"...","date":"..."}`.
- Si le message ne commence pas par `/log `, ne publie rien et ne modifie pas `logs.json`.
- Après une publication, vérifie que `logs.json` reste un JSON valide. Ne modifie pas le design existant de `index.html` pour traiter une commande.
- Le site affiche les logs du plus récent au plus ancien et recharge `logs.json` automatiquement toutes les 10 secondes. Les dates affichées sont formatées en français dans le fuseau `Europe/Paris`.
