# Dashboard_covid_DockerXGrafana

Nous avons ouvert un invit' de commande Ubuntu.  
Puis nous avons crée un dossier grâce à la commande: `mkdir Brief_covid`.  
Ensuite nous sommes rentrés dans le dossier de la manière suivante: `cd Brief_covid`.     
Et enfin nous avons ouvert VS Code avec la commande : `code .`  

Nous avons créé 4 fichiers dans VS Code:

 - fichier python `test.py` -> ouvrir la connection avec MySQL  
 - fichier `Dockerfile` -> paramètrer le code  
 - fichier `docker-compose.yml` -> Créer les containers dans Docker et faire le lien entre la bdd et grafana
 - fichier `devcontainer.json` -> Echange de données

Les trois derniers fichiers ce trouve dans un dossier `.devcontainer`

Voici à quoi ressemble l'arborescence :  
![arborescence](/arborescence.png)

Après cela nous téléchargeons sur VS Code l'extension `VS Code Remote-Containers extension`  
Il permet de créer les containers dans Docker.  
Nous allons par la suite chercher cette extension dans une ` Command Palette`  
Et ouvrir `Remote-Containers: Open Folder in Container ...`  
Cela nous envoie notre dossier dans un Workspace du nom de `Dev Container: Develop Python`  

Nous ouvrons Adminer, qui est une interface graphique de gestion de base de données, sur l'adresse `localhost:8080` et nous connectons avec les données fournies dans `test.py`.  
On importe le fichier `vaccination.sql`    
Après cela nous pouvons ouvrir Grafana grâce au l'adresse `localhost:3000`  
Nous nous connectons, faisons le lien avec la bdd depuis `DATA Sources`  

Pour finir nous avons fait cinq graphiques avec le dashboard.

Voici les graphiques avec leurs requêtes:
![dash1](/dash1.png)  
>SELECT sum(daily_vaccinations), country FROM country_vaccinations GROUP BY country HAVING sum(daily_vaccinations);  


![dash2](/dash2.png)  
>SELECT sum(people_fully_vaccinated), country FROM country_vaccinations GROUP BY country HAVING sum(people_fully_vaccinated); 


![dash3](/dash3.png)
>SELECT  date AS "time", country AS metric, daily_vaccinations FROM country_vaccinations WHERE $__timeFilter(date) ORDER BY date ;   


![dash4](/dash4.png)  
>SELECT daily_vaccinations, date FROM country_vaccinations WHERE country="France";    


![dash5](/dash5.png)  
>SELECT sum(daily_vaccinations), country FROM country_vaccinations GROUP BY country HAVING sum(daily_vaccinations)>10000000;      
