# Système de Gestion Budgétaire UCAD/ESP

## Overview

Ce système de gestion budgétaire est conçu pour l'Université Cheikh Anta Diop (UCAD) et l'École Supérieure Polytechnique (ESP). Il automatise la consolidation budgétaire depuis les besoins départementaux jusqu'à une proposition de budget complète, suivant la méthodologie Unified Process (UP).

## Fonctionnalités Principales

### 🔐 Authentification et Autorisation
- Système d'authentification basé sur les sessions
- Contrôle d'accès basé sur les rôles (RBAC)
- 4 rôles utilisateur : `user`, `chef_dept`, `direction`, `comptable`

### 📊 Gestion Budgétaire
- **Saisie budgétaire** : Interface complète pour créer et modifier les lignes budgétaires
- **Workflow de validation** : Draft → Pending → Validated/Rejected → Consolidated
- **Nomenclature UCAD** : Plus de 70 codes budgétaires prédéfinis
- **Audit trail** : Historique complet des modifications

### 🏢 Consolidation Départementale
- Validation en lot des lignes budgétaires
- Processus d'approbation/rejet avec motifs
- Gestion des éléments en attente
- Mises à jour en temps réel

### 📈 Analyse et Reporting
- Résumé budgétaire avec métriques de performance
- Analyse des écarts (proposé vs réalisé)
- Taux de réalisation et statistiques
- Export Excel/PDF (simulation)

## Architecture Technique

### Stack Technologique
- **Frontend** : React 18 + TypeScript + Vite
- **Backend** : Node.js + Express.js
- **Base de données** : PostgreSQL + Drizzle ORM
- **UI** : Tailwind CSS + shadcn/ui
- **Authentification** : Sessions Express + bcrypt

### Structure du Projet
```
├── client/               # Frontend React
│   ├── src/
│   │   ├── components/   # Composants réutilisables
│   │   ├── pages/        # Pages de l'application
│   │   ├── lib/          # Utilitaires et configuration
│   │   └── hooks/        # Hooks personnalisés
├── server/               # Backend Express
│   ├── db.ts            # Configuration base de données
│   ├── routes.ts        # Routes API
│   ├── storage.ts       # Couche d'accès aux données
│   └── index.ts         # Point d'entrée serveur
├── shared/               # Code partagé
│   ├── schema.ts        # Schémas Drizzle
│   └── budget-codes.ts  # Nomenclature budgétaire
└── attached_assets/      # Documents de référence
```

## Installation et Démarrage

### Prérequis
- Node.js 18+ 
- PostgreSQL
- npm ou yarn

### Configuration
1. Clonez le dépôt
```bash
git clone https://github.com/fmbaye09/UnifiedProcessReporter.git
cd UnifiedProcessReporter
```

2. Installez les dépendances
```bash
npm install
```

3. Configurez la base de données
```bash
# Créez une base de données PostgreSQL
# Configurez la variable d'environnement DATABASE_URL
export DATABASE_URL="postgresql://user:password@localhost:5432/budget_db"
```

4. Initialisez la base de données
```bash
npm run db:push
```

5. Démarrez l'application
```bash
npm run dev
```

L'application sera accessible sur `http://localhost:5000`

## Comptes de Test

- **Admin** : `admin@ucad.edu.sn` / `password`
- **Chef Département** : `chef.esp@ucad.edu.sn` / `password`
- **Utilisateur** : `user.esp@ucad.edu.sn` / `password`

## Workflow Budgétaire

### 1. Saisie Budgétaire
- Les utilisateurs créent des lignes budgétaires (statut : `draft`)
- Sélection de la catégorie selon la nomenclature UCAD
- Saisie des montants proposés et descriptions

### 2. Soumission pour Validation
- Changement du statut vers `pending`
- Apparition dans la queue de consolidation

### 3. Validation Départementale
- Les chefs de département valident ou rejettent
- Passage au statut `validated` ou `rejected`
- Possibilité de validation en lot

### 4. Consolidation Finale
- Agrégation des lignes validées
- Génération du budget final
- Statut `consolidated`

## Sécurité

### Permissions par Rôle
- **user** : Création/modification de ses propres lignes
- **chef_dept** : Validation départementale + accès utilisateur
- **direction** : Accès complet de gestion
- **comptable** : Accès lecture seule pour analyses

### Mesures de Sécurité
- Authentification basée sur les sessions
- Hachage des mots de passe avec bcrypt
- Contrôle d'accès au niveau des routes API
- Validation des données avec Zod
- Protection contre l'injection SQL via Drizzle ORM

## Développement avec Unified Process

Ce projet suit la méthodologie UP avec documentation complète des 4 phases :

1. **Inception** : Définition du périmètre et des exigences
2. **Elaboration** : Architecture et analyse des risques
3. **Construction** : Développement itératif
4. **Transition** : Déploiement et maintenance

## Contribution

Pour contribuer au projet :

1. Forkez le dépôt
2. Créez une branche feature (`git checkout -b feature/nom-fonctionnalite`)
3. Committez vos changements (`git commit -m 'Ajout nouvelle fonctionnalité'`)
4. Poussez vers la branche (`git push origin feature/nom-fonctionnalite`)
5. Ouvrez une Pull Request

## License

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.

## Support

Pour toute question ou problème, veuillez ouvrir une issue sur GitHub ou contacter l'équipe de développement.

---

**Développé avec ❤️ pour l'UCAD/ESP**