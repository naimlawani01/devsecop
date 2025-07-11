# 🚀 DevSecOps Infrastructure

Infrastructure simple pour déployer 3 applications avec Docker.

## 📋 Applications

1. **Application Statique** (HTML/CSS) - Accessible directement sur le port 3000
2. **Django Dashboard** - Derrière reverse proxy sur `/django/`
3. **Flask Application** - Derrière reverse proxy sur `/flask/`

## 🚀 Déploiement

```bash
# Démarrer les services
docker-compose up -d

# Voir les logs
docker-compose logs -f

# Arrêter les services
docker-compose down
```

## 🌐 Accès aux Applications

| Application | URL | Description |
|-------------|-----|-------------|
| **Static App** | http://localhost:3000 | Accès direct pour pentests |
| **Django Dashboard** | http://localhost/django/ | Application Django |
| **Flask App** | http://localhost/flask/ | Application Flask |

## 📁 Structure

```
devsecops/
├── docker-compose.yml          # Infrastructure as Code
├── static-app/                 # Application statique (directe)
├── django-soft-ui-dashboard/   # Application Django
├── flask-datta-1752138310/     # Application Flask
└── nginx/
    └── nginx.conf             # Reverse proxy simple a
``` 