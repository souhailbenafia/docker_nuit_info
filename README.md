# docker_nuit_info

## Les etape pour créer une image docker pour pouvoir build / run votre application dans des containers

### Creer un dossier dont on va creer un fichier :

Dockerfile
Dossier src contient site ou app avec c’est fichier css js etc …

Pour le fichier DockerFile:

### Choisir un serveur
```
FROM nginx:alpine
```


### Copier les donnees du site dans le fichier /usr/share/nginx/html
```
COPY src/* /usr/share/nginx/html
```
### Choisir le port a exposé pour l’image
```
EXPOSE 8080
```
### CMD aide a executer des command  lors de lancement de container dont on va desactiver le daemon pour lancer nginx en foreground.
```
CMD ["nginx", "-g", "daemon off;"]
```
Acceder en dossier qui contient le fichier Dockerfile et lancer le Commandline
### creer une image docker a partir de notre fichier dockerfile et specifier son nom
```
Docker build -t nuitinfo . 
```
### lancer l’image 
```
Docker run -it -p 80:80 nuitinfo
```
### avec les option suivante 
-d :-d=false : mode détaché : exécuter le conteneur en arrière-plan, imprimer un nouvel identifiant de conteneur
-t : Allouer un pseudo-tty
-i : Garder STDIN ouvert même s'il n'est pas connecté
-p : publicPort:InsideDockerPort - 8456:443

Pour tester votre site acceder a localhost:8080
### les etapes  pour le hebergement sur les docker hub
1 Connectez-vous sur https://hub.docker.com/
2 Cliquez sur Créer un référentiel.
3 Choisissez un nom (par exemple verse_gapminder) et une description pour votre référentiel et cliquez sur Créer.
4 Connectez-vous au Docker Hub depuis la ligne de commande
```
docker login --username=yourhubusername --email=youremail@company.com
```

### juste avec votre propre nom d'utilisateur et e-mail que vous avez utilisé pour le compte. Entrez votre mot de passe lorsque vous y êtes invité. Si tout a fonctionné, vous recevrez un message similaire à
```
WARNING: login credentials saved in /home/username/.docker/config.json
Login Succeeded
```
5 Vérifiez l'ID de l'image à l'aide deet taguez votre image
```
docker images
docker tag bb38976d03cf yourhubusername/verse_gapminder:firsttry
```

Poussez votre image vers le référentiel que vous avez créé
```
docker push yourhubusername/verse_gapminder
```



