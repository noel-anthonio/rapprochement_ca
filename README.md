# Rapprochement CA — déploiement Vercel

## Fichiers requis

- `index.html` : page d'entrée qui redirige vers l'application avec un chemin relatif.
- `rapprochement-ca.html` : application principale.

Les deux fichiers doivent rester au même niveau dans le dossier publié.

## Tester localement

Décompressez le paquet et ouvrez `index.html` dans le navigateur. Il redirige vers `rapprochement-ca.html` à l'aide d'un chemin relatif.

Pour tester Google OAuth / Google Drive, utilisez plutôt un serveur local, par exemple depuis ce dossier :

```powershell
python -m http.server 8000
```

Puis ouvrez `http://localhost:8000/rapprochement-ca.html`.

## Publier sur Vercel

Placez ces fichiers à la racine du dépôt ou du dossier de sortie de Vercel. Pour une application HTML statique, utilisez le preset `Other` et vérifiez que le répertoire de sortie pointe vers le dossier contenant `index.html` et `rapprochement-ca.html`.
