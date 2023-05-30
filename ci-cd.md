## Cloner un repo sur un serveur distant

1. En SSH, se connecter et se placer dans le dossier où le repo sera
1. Générer une clef SSH pour pouvoir gérer la connexion entre le serveur et GitHub par la suite
  Par exemple : 
  > ssh-keygen -t ed25519 -C "your-email@example.com"

  ```ssh-keygen```: commande pour générer une clef SSH (système Unix-like, Linux - macOS)
  
  ```-t ed25519```: spécifie le type de clef à générer. ```ed25519``` => algorithm Ed25519, elliptic curve algorithm
1. Copier la clef publique (en SSH ou FTP)
  > cat ~/.ssh/id_ed25519.pub
1. Ajouter la clef au compte GitHub (https://github.com/settings/ssh/new)
2. Tester la connexion avec GitHub et vérifier le fingerprint : 
  > ssh -T git@github.com
3. On peut désormais lancer les commandes git clone, git fetch...