# Système de Notation d'Événements - Relais & Châteaux

## 📋 Description du projet

Application web de gestion de notation d'événements avec système de rôles et modération.

## 🛠️ Technologies utilisées

- **Framework**: Symfony 7.0
- **Base de données**: MySQL/MariaDB
- **Architecture**: MVC
- **Authentification**: Symfony Security Bundle
- **ORM**: Doctrine
- **Interface Admin**: EasyAdmin (optionnel)

## 👥 Rôles utilisateurs

### 1. Utilisateur standard (ROLE_USER)
- Consulter les événements
- Publier des avis
- Modifier ses propres avis

### 2. Responsable d'événement (ROLE_RESPONSABLE)
- Toutes les fonctionnalités utilisateur
- Gérer ses événements
- Modérer les avis de ses événements

### 3. Administrateur (ROLE_ADMIN)
- Accès complet
- Gérer tous les utilisateurs
- Gérer tous les événements
- Modérer tous les avis

## 📦 Installation

### Prérequis
- PHP 8.2 ou supérieur
- Composer
- MySQL/MariaDB
- Serveur web (Apache/Nginx)

### Étapes d'installation

1. **Cloner le projet**
```bash
git clone [votre-repo]
cd event-rating-app
```

2. **Installer les dépendances**
```bash
composer install
```

3. **Configurer la base de données**
```bash
# Éditer le fichier .env
DATABASE_URL="mysql://user:password@127.0.0.1:3306/event_rating_db"
```

4. **Créer la base de données**
```bash
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
```

5. **Charger les données de test (fixtures)**
```bash
php bin/console doctrine:fixtures:load
```

6. **Lancer le serveur**
```bash
symfony server:start
# ou
php -S localhost:8000 -t public/
```

## 🔐 Identifiants de test

### Administrateur
- **Email**: admin@relaischateaux.com
- **Mot de passe**: Admin123!

### Responsable d'événement
- **Email**: responsable@relaischateaux.com
- **Mot de passe**: Resp123!

### Utilisateur standard
- **Email**: user@relaischateaux.com
- **Mot de passe**: User123!

## 📁 Structure du projet

```
event-rating-app/
├── config/              # Configuration Symfony
├── src/
│   ├── Controller/      # Contrôleurs
│   ├── Entity/          # Entités Doctrine
│   ├── Form/            # Formulaires
│   ├── Repository/      # Repositories
│   └── Security/        # Authentification
├── templates/           # Vues Twig
├── public/              # Fichiers publics
└── var/                 # Cache et logs
```

## 🎯 Fonctionnalités principales

### Gestion des événements
- Liste des événements avec filtres
- Détails d'un événement
- Affichage des avis modérés

### Gestion des avis
- Publication d'avis (utilisateurs authentifiés)
- Modification de ses propres avis
- Modération par responsable/admin
- Visibilité conditionnelle (avis non modérés invisibles)

### Dashboard
- Interface adaptée selon les droits
- Statistiques pour les responsables
- Gestion complète pour les admins

## 📊 Modèle de données

### Entités principales
- **Utilisateur**: Gestion des comptes et rôles
- **Événement**: Informations sur les événements
- **Avis**: Notes et commentaires avec modération
- **Responsable**: Association utilisateur-événement

### Relations
- Un utilisateur peut créer plusieurs avis (1,n)
- Un événement peut avoir plusieurs avis (1,n)
- Un avis est modéré par le responsable de l'événement (règle 1)

## ⚙️ Règles de gestion implémentées

1. ✅ Un utilisateur ne peut modifier que ses propres avis
2. ✅ Un avis ne peut être modéré que par le responsable de l'événement ou un administrateur
3. ✅ Un avis non modéré n'est pas visible par les autres utilisateurs

## 🚀 Commandes utiles

```bash
# Créer un nouvel utilisateur
php bin/console app:create-user

# Nettoyer le cache
php bin/console cache:clear

# Mettre à jour le schéma de la base
php bin/console doctrine:schema:update --force

# Voir les routes
php bin/console debug:router
```

## 📝 Choix techniques

### Pourquoi Symfony ?
- Framework mature et robuste
- Excellente gestion de la sécurité
- Architecture MVC claire
- Large écosystème de bundles

### Architecture MVC
- **Modèle**: Entités Doctrine avec validation
- **Vue**: Templates Twig réutilisables
- **Contrôleur**: Logique métier séparée

### Sécurité
- Hashage des mots de passe avec bcrypt
- Protection CSRF sur les formulaires
- Validation des données côté serveur
- Contrôle d'accès par rôles (voters)

## 🐛 Difficultés rencontrées et solutions

### 1. Gestion de la modération
**Problème**: Visibilité conditionnelle des avis
**Solution**: Ajout d'un champ `estModere` avec filtre dans les requêtes

### 2. Permissions complexes
**Problème**: Un utilisateur peut modifier ses avis, un responsable peut modérer
**Solution**: Utilisation de Voters Symfony pour une logique fine

### 3. Dashboard adaptatif
**Problème**: Interface différente selon les rôles
**Solution**: Templates modulaires avec héritage Twig

## 📈 Évolutions possibles

- [ ] Système de notifications par email
- [ ] Export des avis en PDF/Excel
- [ ] Statistiques avancées pour les responsables
- [ ] API REST pour application mobile
- [ ] Système de tags pour les événements

 N° matricule: [Votre matricule]