# Réalisation

## Infra

- Configurer un nouveau Security Group (service EC2 -> security groups)
  - Ouvert sur le port 22 à partir de Anywhere (ssh)
  - Ouvert sur le port 80 à partir de Anywhere (http)
  - Ouvert sur le port 3001 à partir de Anywhere (http)
- Lancer 2 instances EC2 et configurez les pour utiliser le security group que vous avez créé

## Backend

- Mettre le backend fourni sur un repo GitHub **PUBLIC**
  - N'oubliez pas de NE PAS commiter les node_modules ;)
- Se connecter sur une des deux EC2, qui sera la machine du backend
- Se mettre en **root** avec `sudo su`
- Installer git, voici comment faire:
  - https://cloudaffaire.com/how-to-install-git-in-aws-ec2-instance/
- cloner le backend maintenant sur votre repo git
- Installer npm (via nvm)
  - https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-up-node-on-ec2-instance.html
- Installer les packages du backend et démarrer le server
- Vérifiez que vous êtes en mesure de toucher le serveur, sur votre navigateur, sur le port 3001 (faites attention au "http" vs "https")

## Frontend

- Commencez par changer l'url dans le fichier `.env` pour celui de votre machine backend, puis démarrez et testez le frontend pour voir s'il touche bien la machine EC2
- Le frontend est un environnement de développement create-react-app. Ce n'est pas souhaitable en production. On veut déployer un serveur express livrant notre frontend de manière statique.
  - `npm run build` vous donne un bundle dans le répertoire `build`
  - Copiez le contenu de ce répertoire dans le répertoire `public` de frontendStatic.
- Une fois que ça fonctionne, répétez les étapes pour la 2e machine EC2 de manière à cloner et démarrer votre frontend sur la 2e machine.
- Une fois que ça fonctionne et que votre application est utilisable, laissez vos terminaux rouler et demandez au prof de valider votre travail.

## Attention

L'url du DNS public des machines que vous donne amazon utilise le protocol HTTPS, faites attention d'enlever le "s" de l'url pour toucher vos machines.

Vous ne pourrez pas toucher au port 3000 du frontend. Il faut configurer le frontend, sur la machine EC2, pour utiliser le port 80 pour le serveur de dévellopement. Pour ce faire, vous devez faire `export PORT=80` avant le démarrage.
