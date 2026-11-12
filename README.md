# mes-skills-claude

Ce dépôt héberge mes skills pour Claude Code. Une skill est un petit dossier
(un fichier `SKILL.md` + éventuellement des scripts) qui apprend à Claude à
faire une tâche précise.

## Skill `public-apis`

Dossier : [`public-apis/`](public-apis/)

Cette skill permet à Claude de répondre aux questions qui demandent des données
en direct (météo, taux de change, cryptomonnaies, jours fériés, livres,
Wikipédia, etc.). Pour cela, elle :

1. cherche une API gratuite adaptée dans la liste communautaire
   [public-apis](https://github.com/public-apis/public-apis) (environ 1 400 API,
   téléchargées et gardées en cache 24 h) ;
2. appelle cette API **en sécurité** : lecture seule (GET), HTTPS obligatoire,
   pas d'accès au réseau interne, taille et durée de réponse limitées ;
3. répond en français, en citant la source.

Les API sans clé sont toujours préférées. Aucune clé n'est stockée dans ce
dépôt.

Fichiers :

- `SKILL.md` : les instructions pour Claude ;
- `search_apis.py` : le script de recherche et d'appel sécurisé (Python 3,
  aucune dépendance à installer).

### Installation à la main

La skill doit se trouver dans `~/.claude/skills/public-apis/` pour être
disponible dans tous vos projets. Dans un terminal :

```bash
mkdir -p ~/.claude/skills/public-apis
cd ~/.claude/skills/public-apis
curl -fsSLO https://raw.githubusercontent.com/stephenogoudedji/mes-skills-claude/main/public-apis/SKILL.md
curl -fsSLO https://raw.githubusercontent.com/stephenogoudedji/mes-skills-claude/main/public-apis/search_apis.py
```

Relancez ensuite Claude Code : la skill est chargée automatiquement.

Pour vérifier que tout marche :

```bash
python3 -I ~/.claude/skills/public-apis/search_apis.py --call "https://api.frankfurter.dev/v1/latest?from=EUR&to=USD"
```

Vous devez voir le taux de change euro → dollar.

### Mise à jour

Relancez simplement les deux commandes `curl` ci-dessus.

## Sources et crédits

- La skill `public-apis` s'appuie sur la liste communautaire
  [public-apis](https://github.com/public-apis/public-apis), publiée sous
  licence MIT par ses contributeurs. Cette liste n'est pas recopiée dans ce
  dépôt : le script la télécharge depuis son dépôt d'origine au moment de
  l'utilisation.
- Ce dépôt n'est pas affilié au projet public-apis ni aux services cités.
- Chaque API appelée reste la propriété de son auteur et est soumise à ses
  propres conditions d'utilisation (limites de requêtes, mention de la
  source, etc.).
