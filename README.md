# Rapprochement CA

Application HTML pour importer les données, rapprocher le chiffre d’affaires et conserver un historique des rapprochements.

## Fichiers

- `rapprochement-ca.html` : l’application.
- `README.md` : ce guide.

## Démarrer l’application sur Windows

1. Placez `rapprochement-ca.html` dans un dossier sur votre ordinateur.
2. Ouvrez ce dossier dans l’Explorateur de fichiers.
3. Cliquez dans la barre d’adresse, tapez `powershell`, puis appuyez sur Entrée.
4. Exécutez :

   ```powershell
   python -m http.server 8000
   ```

5. Laissez la fenêtre PowerShell ouverte et ouvrez dans Chrome :

   <http://localhost:8000/rapprochement-ca.html>

Python doit être installé. Si le port 8000 est déjà utilisé, choisissez un autre port et utilisez la même adresse/port dans la configuration Google Cloud.

## Importer les données

Dans l’application, importez les fichiers source `DATA_RENTA_COUT` et référence `BUDGET | CA REALISEE`. Les fichiers `.xlsx`, `.xls` et `.csv` sont pris en charge.

Le rapprochement utilise la colonne **Corresp clés**. Avant d’insérer une clé dans la base de référence, vérifiez qu’elle n’y existe pas déjà.

## Configurer Google Drive (facultatif)

1. Ouvrez la [Google Cloud Console](https://console.cloud.google.com/) et créez ou sélectionnez un projet.
2. Activez **Google Drive API**.
3. Dans **Google Auth Platform**, configurez l’écran de consentement. En mode test, ajoutez votre compte Google comme utilisateur de test.
4. Créez un identifiant OAuth de type **Application Web**.
5. Dans **Origines JavaScript autorisées**, ajoutez exactement :

   `http://localhost:8000`

6. Copiez le **Client ID** généré (il se termine par `.apps.googleusercontent.com`).
7. Dans l’application, ouvrez **Historique**, collez ce Client ID dans le panneau Google Drive et cliquez sur **Enregistrer les paramètres**.
8. Cliquez sur **Connecter / synchroniser Drive**, puis connectez-vous à votre compte Google et autorisez l’accès demandé.

N’inscrivez jamais de mot de passe ni de secret client dans le fichier HTML. La connexion Google doit être relancée après un rechargement de la page si la session a expiré.

## Où se trouvent les archives ?

Avec Google Drive connecté, l’application crée le dossier **Mon Drive / Archives rapprochement CA** et y enregistre deux fichiers par archive :

- `Rapporchement_CA_2026_Aout.xlsx` : synthèse et lignes archivées dans Excel ;
- `Rapporchement_CA_2026_Aout.json` : archive complète en JSON.

L’année et le mois varient selon l’archive. Si plusieurs archives portent sur le même mois, un suffixe est ajouté afin de conserver les versions précédentes.

Une archive est d’abord conservée dans le navigateur. Si Google Drive n’est pas connecté ou si l’envoi échoue, la copie locale reste disponible ; reconnectez Drive et relancez la synchronisation depuis **Historique**.

## Sauvegarde et migration

Dans **Historique**, utilisez **Exporter sauvegarde locale (JSON)** pour sauvegarder l’historique ainsi que les données actives. Utilisez ensuite **Importer sauvegarde JSON** pour restaurer ces données.

Important : le stockage du navigateur pour un fichier ouvert en `file://` est séparé de celui de `http://localhost`. Si vous passez du double-clic au serveur local, exportez d’abord la sauvegarde JSON depuis l’ancienne ouverture, puis ouvrez l’application sur `localhost` et importez la sauvegarde avant la première synchronisation.

## Conseils

- Vérifiez qu’une archive apparaît dans le dossier Google Drive après la synchronisation.
- Gardez une copie externe des sauvegardes importantes.
- Ne supprimez pas les anciennes données avant d’avoir vérifié leur sauvegarde.
