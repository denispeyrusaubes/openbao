# Étape 1: Construction de l'application Ember avec Yarn
FROM node:16 AS builder

# Répertoire de travail dans le conteneur
WORKDIR /app

# Copier les fichiers package.json et yarn.lock pour installer les dépendances
COPY package.json yarn.lock ./

# Installer les dépendances sans générer de cache local pour économiser de l'espace
RUN yarn install 

# Copier le reste des fichiers de l'application
COPY . .

# Construire l'application Ember pour l'environnement de production
RUN yarn build --environment=production

# Étape 2: Utilisation de Nginx pour servir l'application
FROM nginx:alpine

# Copier la build générée dans le répertoire de distribution d'Ember vers Nginx
COPY --from=builder /app/dist /usr/share/nginx/html

# Supprimer la configuration par défaut de Nginx et ajouter la configuration spécifique
#RUN rm /etc/nginx/conf.d/default.conf
#COPY nginx.conf /etc/nginx/conf.d/

# Exposer le port 80 pour l'application
EXPOSE 80

# Commande pour démarrer Nginx
CMD ["nginx", "-g", "daemon off;"]
