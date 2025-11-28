FROM nginx:alpine

# Suppression de la config par défaut pour éviter les conflits
RUN rm /etc/nginx/conf.d/default.conf

# Copie de notre configuration personnalisée
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copie des fichiers du site
COPY index.html /usr/share/nginx/html/
COPY style.css /usr/share/nginx/html/
COPY script.js /usr/share/nginx/html/

EXPOSE 80
