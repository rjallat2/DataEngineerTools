# DatavizPython

*Introduction* 

Pour notre projet de DataEngineer Tools nous avons décidé de nous intéresser aux biens immobilier à vendre dans les 10 plus grandes villes de France disponiblesur le site particulieraparticulier.fr ([lien](https://www.pap.fr/annonce/vente-maisons-paris-75-g439)) 

Nous avons donc scrappé les informations concernant les maisons à vendre sur le site en question en nous focalisant sur le prix, la taille (en m2), le nombre de chambre, le nombre de pièce et la localisation avec la ville et le code postal. 

L’enjeu ici est de permettre aux utilisateurs une meilleure visualisation du marchés immobilier actuel à l'aide de plusieurs indicateurs/visualisation différent.
En effet en parcourant les nombreuses pages d'offre sur les sites d'agences immobilières il est facile de se perdre. Notre but est donc de proposer une vue globale de ce qui est disponible en ce moment pour pouvoir adapter sa demande en fonction de ce qui est le plus rentable et le mieux pour soit.  


« Le réchauffement climatique est le constat d’une augmentation de la température terrestre moyenne sur de longues périodes » 
En effet il s’agit d’étudier ici les variations de température pour l’ensemble du globe et sur des temps longs (étude du climat à grande échelle) et non la variabilité des températures à l’échelle de quelques jours ou sur une saison (prévisions météorologiques) afin de constater ce dérèglement climatique et de prendre conscience de la réalité de cette catastrophe. 

En effet cela entraine des crises sanitaires, écologiques et humanitaires que nous pouvons déjà observer, il est donc de notre devoir de changer les choses pour atténuer cette tendance.

Pour procédé aux visualisations nous avons donc utilisés comme dit précédemment 2 jeux de données (disponible sur Kaggle) : city_temperature.csv([lien_kaggle](https://www.kaggle.com/sudalairajkumar/daily-temperature-of-major-cities)) et worldcities.csv ([lien_kaggle](https://www.kaggle.com/juanmah/world-cities))que nous avons mergé en fonction des villes afin d’avoir les températures quotidiennes des grandes villes du monde de 1995 à 2020 avec leur coordonnées GPS respectives.

Nous obtenons donc une dataframe df contenant comme variables : 
-	Region : ['Africa', 'Asia', 'Australia/South Pacific', 'Europe',  'Middle East', 'North America', 'South/Central America & Carribean']
-	Country : 97 Pays différents 
-	City : 128 grandes villes différentes
-	Month : Mois de l’année (de janvier 01 à décembre 12) 
-	Day : Jours d’un mois 
-	Year : de 1995 à 2020
-	AvgTemperature : Température en moyenne quotidienne en Kelvin (que nous avons convertie en dégrès pour que ça soit plus parlant) 
-	lat : latitude de la ville en question 
-	lng : longitude de la ville en question 

<br>

### La récupération des données


Nos données sont issues de Kaggle.com, ainsi pour pouvoir les récupérer, il faut se connecter avec un compte.
Pour récupérer directement les données sur internet nous devons utiliser l’API de Kaggle, pour cela nous devons obtenir un token et grâce à ce token nous pouvons directement récupérer les données sur notre machine.
Afin d’éviter d’avoir plusieurs erreurs et améliorer la performance de notre code nous avons décidé de mettre les jeux de données localement avec notre code.
<br>

### User Guide

*Installation*

Pour pouvoir avoir accès au dashboard il vaus faut suivre les étapes suivantes : 


*  Copier le projet sur votre machine grace à la commande :

* [ ]  `$ git clone https://git.esiee.fr/kulaveen/projet_python_e4`

* Verifiez que les fichiers suivant soit dans le même repertoire : 

* [ ]  `city_temperature.csv`
* [ ]  `worldcities.csv`
* [ ]  `main.py`

*  Sur VisualStudioCode ouvrir le projet que vous venez de téléchargé : File > Open Folder... séléctionner le fichier téléchargé

* Avant de pouvoir lancer le projet il faut au préalable installer les packages nécéssaires. Pour cela taper les commande suivantes dans votre console : 

* [ ]  `pip install dash`

* [ ]   `pip install plotly`

* [ ]  `pip install pandas`

* [ ]  `pip install numpy`

* [ ]  `pip install seaborn`

* A partir du Terminal sous VisualStudioCode lancer le script grace à la command e

* [ ] `python3 main.py` pour Linux
* [ ] `python main.py`  pour Windows

* A la fin de l'éxécution du script, l'adresse http://127.0.0.1:8050/ est renvoyée. Utilisez cette adresse pour visualiser le DashBoard.


<br>


### Developper Guide

Pour comprendre le programme, nous allons nous intéresser à quatre points qui sont le **traitement de données**, **les figures**, **le layout** et **les callbacks/updates**.

**Traitement de données**:
Cette étape est primordiale pour le bon déroulement du projet, cela se passe directement après les imports et commence avec des *pd.read_csv*.
*pd.read_csv* permet d’ouvrir et visualiser les dataframes
On abandonne les colonnes qui ne nous sont pas intéressante avec un *.drop*
C’est là qu'on créer plusieurs sous dataframe afin de pouvoir les utiliser sans modifier notre dataframe mère.
On joint différent dataframe entre eux mais qui possède au moins une colonne commune grâce à *pd.merge*
Ainsi si vous voulez étudier d'autres caractéristiques de notre base de données , il vous faudra surement d’abord créer un sous dataframe sur lequel vous voulez travailler .

**Les figures**:
Cette partie du code se trouve juste après *app=dash.Dash(_name_)*  et avant le layout. C’est ici que sont défini les graphiques à tracer grâce à plotly express avec *px.line*,*px.scatter*,*px.histogram*   
Ainsi, si vous voulez ajouter des figures, graphiques, c’est dans cette partie que vous devez les définir.

**Le layout**:
app.layout permet de structurer le dashboard et décide de ce qui doit être affiché sur l’écran de l’utilisateur.
Dans cette partie on a :
- le titre du dashboard avec *html.H1*
- les description et les zones de textes avec *html.Div*
- la représentation du début de notre dashboard avec *dash_table.DataTable*
- la représentation des figures que l’on a définit plus avec *dcc.Graph*
- des dropdowns avec *dcc.Dropdow*n
- des slider avec *dcc.Slider*
Ainsi si vous voulez modifier l’affichage du dashboard, c’est ici qu’il faut faire des mofications

**Les callbacks/updates**:
Cette partie est l’élément clé pour avoir un dashboard interactif.
- *@app.callback()* indique quels sont les inputs et outputs à prendre en compte et à actualiser, pour cela, les graphiques ou encore les dropdown/slider possède des id que l’on définit lors de leur création dans le layout. Ces id sont données en argument pour les inputs et outputs.
- *update_figure()* prend en argument le nombre d' inputs défini dans le *@app.callback()* qui seront par ailleurs traités dans l’ordre d’apparition dans le callback et retourne le même nombre d'éléments que de outputs défini dans le callback.

### Rapport d'analyse

*Conclusion*

L'Organisation météorologique mondiale a annoncé que les 10 années se terminant à partir de fin 2019 sont les 10 années les plus chaudes de l'histoire mondiale.
En effet avec nos visualisations nous avons pu observer que la température moyenne mondiale augmente de façon alarmante au cours des deux dernières décennies. 
En analysant les graphiques on observe que toutes les régions sont touchées par ce réchauffement climatique dans une certaine mesure. Dans certaines régions, la température a augmenté plus rapidement, les cas les plus notoires sont : l'Asie, le Moyen-Orient, l'Amérique du Nord et l'Europe. En effet il s'agit des régions les plus développées donc avec une dynamique économique élévée (industries lourdes, import, export, ...) .
Il est également possible de voir que l'année 2019 est, dans la plupart des cas, celle qui a la température moyenne maximale.

Comme vous le savez nous traversons actuellement une grave crise sanitaire dû à la pandémie du Covid-2019 apparue en novembre 2019 et qui a entrainé le monde dans un effondrement de l’activité économique et humaine dû à des mesures de confinement, de distanciation imposée par les États pour palier a cette épidémie. 
Il serait donc intéressant, lorsque ce dataset sera mis à jour, de voir quel impact a eu cette crise sur les températures des années suivantes, et si elle a permis de réduire la vitesse du réchauffement climatique. 

Il serait également intéressant de pouvoir utilisé ce jeu de données pour pouvoir prédire l’évolution des températures dans les années à venir pour avoir une idée de ce qui nous attend si nous n’agissons pas maintenant. 
Pour cela nous pourrions utiliser les années 1995 à 2014 comme données d’entrainement et valider notre algorithme grâces aus données des années 2015 à 2019. 





Dans le cadre de notre projet DataEngineerTools nous avons créé une application web 
Nous avons fais le choix de nous interesser aux biens immobiliers à vendre dans les 10 plus grandes villes de France proposé par le site Particulier a particulier. 

Nous avons donc scrappé les informations concernant les maisons à vendre sur le site en question en nous focalisant sur le prix, la taille (en m2), le nombre de chambre, le nombre de pièce et la localisation avec la ville et le code postal. 

