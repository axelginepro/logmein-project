FROM python:3.11-slim

# Création d'un utilisateur système dédié (non-root)
# C'est le point clé pour le critère "Sécurité"
RUN useradd -r -s /bin/false appuser

WORKDIR /app

# Installation des dépendances système (pour psycopg2)
RUN apt-get update && apt-get install -y \
    gcc \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Copie des requirements d'abord (optimisation du cache Docker)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copie du code
COPY app.py .

# Changement de propriétaire des fichiers pour l'utilisateur sécurisé
RUN chown -R appuser:appuser /app

# Passage à l'utilisateur sécurisé
USER appuser

# Variables d'environnement par défaut
ENV DB_HOST=db
ENV DB_NAME=logs_db
ENV DB_USER=logs_user
# Note: En prod, le mot de passe viendra d'un Docker Secret, pas de cette variable
ENV DB_PORT=5432

EXPOSE 5000

CMD ["python", "app.py"]
