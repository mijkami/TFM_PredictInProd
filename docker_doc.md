# DOCKERFILE

## Exemple de Dockerfile complet (fichier "Dockerfile" à placer à la racine):
FROM python:3.8.6-buster
COPY api /api
COPY requirements.txt /requirements.txt
COPY model.joblib /model.joblib
COPY TaxiFareModel /TaxiFareModel
RUN pip install --upgrade pip
RUN pip install -r requirements.txt
CMD uvicorn api.fast:app --host 0.0.0.0

## Détails:
### installer template docker avec linux + python
FROM python:3.8.6-buster

### copier les fichiers nécessaires
### 1er argument :SOURCE (fichier à copier)
### 2ème argument: CIBLE, endroit où copier)
COPY api /api                               
COPY requirements.txt /requirements.txt
COPY model.joblib /model.joblib
COPY TaxiFareModel /TaxiFareModel

### lancer les installations de librairies dans le container
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

## lancer une commande 
## (serveur "uvicorn", dossier "api", fichier "fast", fonction "app", à l'adresse localhost / 0.0.0.0)
CMD uvicorn api.fast:app --host 0.0.0.0




# TERMINAL

## lancer daemon service docker (plus important)
sudo systemctl start docker

## arrêter daemon service docker
sudo systemctl stop docker

## activer à chaque démarrage daemon service docker
sudo systemctl enable docker

## désactiver démarrage auto au boot du daemon service docker
sudo systemctl disable docker 

## afficher images docker
sudo docker images

## créer un container avec le nom IMAGE_ID de son choix à la racine 
## (attention créer "Dockerfile" nécessaire)
sudo docker build -t IMAGE_ID .   

## exécuter docker interactivement (rentrer dans le terminal)
## (autre version:) sudo docker run -it IMAGE_ID sh
sudo docker run -it -e PORT=8000 -p 8000:8000 IMAGE_ID sh

## run image (mise en route image/container)
sudo docker run -it -e PORT=8000 -p 8000:8000 IMAGE_ID  

## effacer image docker
sudo docker rmi IMAGE_ID

## effacer "mode brute" (même si instance en cours d'execution)
sudo docker rmi IMAGE_ID -f

# voir les instances
sudo docker ps

# arrêter une image en cours d'execution
sudo docker stop IMAGE_ID