## Cloner un repo sur un serveur distant

- En SSH, se connecter et se placer dans le dossier où le repo sera
- Générer une clef SSH pour pouvoir gérer la connexion entre le serveur et GitHub par la suite. **Attention au changement de nom, le path doit RESTER LE MÊME*
  Par exemple : 
    > ssh-keygen -t ed25519 -C "your-email@example.com"

  ```ssh-keygen```: commande pour générer une clef SSH (système Unix-like, Linux - macOS)
  
  ```-t ed25519```: spécifie le type de clef à générer. ```ed25519``` => algorithm Ed25519, elliptic curve algorithm
- Copier la clef publique (en SSH ou FTP)
    > cat ~/.ssh/id_ed25519.pub
- Ajouter la clef au compte GitHub (https://github.com/settings/ssh/new) avec le compte de l'entreprise ou non, propriétaire du dossier
- Tester la connexion avec GitHub et vérifier le fingerprint, sur le serveur dans le dossier : 
    > ssh -T git@github.com
- On peut désormais lancer les commandes git clone, git fetch...

## Deploy avec SSH et RSYNC avec les GitHub Actions

Pour déployer via les github actions, il nous faudra une nouvelle clef SSH.

- En SSH, se connecter avec le compte et rester dans le dossier d'accueil
- Se placer dans le dossier .ssh ou le créer s'il n'existe pas
- Générer une clef SSH avec la commande suivante : 
    > ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
  
  La clef publique possède l'extension .pub, alors que la clef privée n'en a pas.
- Ajouter la clef publique dans `authorized_keys` pour que les machines avec la clef privée puissent accéder au serveur.
    > cat id_rsa.pub >> ~/.ssh/authorized_keys
- Ajouter la clef privée dans les Secrets du repo
  - Titre : `SSH_PRIVATE_KEY`
  - Contenu : copier le contenu du fichier sans extension (id_rsa)

Pour la GitHub action, on va utiliser le package `shimataro/ssh-key-action@v2`. 

Voir la GitHub action ici : https://github.com/Aimee-RTLNG/docs/blob/main/examples/deploy_ssh.yml 
