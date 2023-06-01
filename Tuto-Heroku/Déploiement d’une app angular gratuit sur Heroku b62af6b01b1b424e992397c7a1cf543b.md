# Déploiement d’une app angular gratuit sur Heroku

# 1 : Créer l’application sur Heroku

- Créer un compte Heroku
- Créer une application (code de CB requis, mais service gratuit dans cet exemple)
    
    ![Capture d’écran 2023-06-01 à 10.54.02.png](De%CC%81ploiement%20d%E2%80%99une%20app%20angular%20gratuit%20sur%20Heroku%20b62af6b01b1b424e992397c7a1cf543b/Capture_decran_2023-06-01_a_10.54.02.png)
    
    ![Capture d’écran 2023-06-01 à 10.55.32.png](De%CC%81ploiement%20d%E2%80%99une%20app%20angular%20gratuit%20sur%20Heroku%20b62af6b01b1b424e992397c7a1cf543b/Capture_decran_2023-06-01_a_10.55.32.png)
    
- Nous allons voir la méthode de déploiement via GitHub bien que la méthode via Heroku CLI soit également intéressante 

connectez l’app à un repo gitHub et cliquez sur Enable Automatic Deploys sur la branche main.
    
    ![Capture d’écran 2023-06-01 à 10.57.35.png](De%CC%81ploiement%20d%E2%80%99une%20app%20angular%20gratuit%20sur%20Heroku%20b62af6b01b1b424e992397c7a1cf543b/Capture_decran_2023-06-01_a_10.57.35.png)
    

# 2 : Préparer le projet

**Nous allons déployer l’application à chaque fois que la branche main est mise à jour.**

Assurez-vous de travailler sur une branche de développement et d’envoyer votre code sur main **(étape 3)** uniquement lorsque toutes les étapes suivantes sont effectués, et que votre code est prêt pour la production.

- Une fois votre application Angular prête à être déployé, ajouter express au dépendances :
    
    ```jsx
    npm i express
    ```
    
- Créer un fichier server.js à la racine du projet contenant le code suivant en remplaçant “/dist/final-brief-weather” part “dist/nom-du-repo-github” aux lignes 6 et 9 : 
    
    ```jsx
    const express = require("express");
    const path = require("path");
    
    const app = express();
    
    app.use(express.static(__dirname + "/dist/final-brief-weather"));
    
    app.get("/*", function (req, res) {
      res.sendFile(path.join(__dirname + "/dist/final-brief-weather/index.html"));
    });
    
    app.listen(process.env.PORT || 8080);
    ```
    
- Créer un fichier Procfile sans extension (pas de .qqchose) à la racine du projet. 
A l’intérieur du fichier on ajoute uniquement une ligne :
    
    ```jsx
     web: npm start
    ```
    
- Modifier name pour que le nom match avec celui donné à l’app heroku, et scripts ainsi dans le fichier package.json :

```
{
  "name": "your-app-name-disponible",
  ...
  "scripts": {
    "start": "node server.js",
    "build": "ng build"
  },
...
}
```

# 3 : Merge branche de la branche de développement sur main et push.

Et c’est tout ! 

L’application est maintenant en ligne, 
elle sera mise à jour a chaque push de main.

Vous pouvez y accéder en cliquant sur Open app.

![Capture d’écran 2023-06-01 à 11.11.25.png](De%CC%81ploiement%20d%E2%80%99une%20app%20angular%20gratuit%20sur%20Heroku%20b62af6b01b1b424e992397c7a1cf543b/Capture_decran_2023-06-01_a_11.11.25.png)
