# eBooks Payment Callback Page

Page de redirection pour les paiements MoneyFusion (Wave CI, Orange Money, etc.) vers l'application mobile eBooks.

## 🎯 Objectif

Cette page sert de pont entre les systèmes de paiement mobile (qui nécessitent une URL HTTPS) et l'application React Native (qui utilise des deep links `ebooks://`).

## 🔄 Fonctionnement

1. L'utilisateur effectue un paiement via Wave CI dans l'app eBooks
2. Wave CI redirige vers cette page : `https://[your-github-pages-url]/?token=xxx&...`
3. Cette page capture automatiquement tous les paramètres
4. Redirection automatique vers : `ebooks://payment-callback?token=xxx&...`
5. L'application eBooks vérifie le paiement et ajoute le livre à la bibliothèque

## 📋 Installation

### 1. Créer un nouveau repo GitHub

```bash
# Initialiser git
cd payment-callback-page
git init
git add .
git commit -m "Initial commit: Payment callback page for eBooks app"
```

### 2. Créer le repo sur GitHub

Créez un nouveau repo sur GitHub (ex: `ebooks-payment-callback`) puis :

```bash
git remote add origin https://github.com/[votre-username]/ebooks-payment-callback.git
git branch -M main
git push -u origin main
```

### 3. Activer GitHub Pages

1. Allez dans **Settings** > **Pages**
2. Source : **Deploy from a branch**
3. Branch : **main** / **(root)**
4. Sauvegardez

### 4. Mettre à jour l'URL dans l'app

Dans `app/services/paymentService.ts`, mettez à jour :

```typescript
const RETURN_URL = 'https://[votre-username].github.io/ebooks-payment-callback/';
```

## 🧪 Test

Pour tester que la page fonctionne :

```
https://[votre-username].github.io/ebooks-payment-callback/?token=test123&status=paid
```

La page devrait se charger et tenter de rediriger vers `ebooks://payment-callback?token=test123&status=paid`

## 🎨 Caractéristiques

- ✅ Design moderne et responsive
- ✅ Animation de chargement
- ✅ Redirection automatique vers l'app
- ✅ Bouton manuel de secours
- ✅ Support de tous les paramètres URL
- ✅ Logs de debug dans la console
- ✅ Compatible mobile et desktop

## 📱 Deep Link

Le deep link utilisé est : `ebooks://payment-callback`

Ce lien doit être configuré dans l'app React Native (`app.json` ou `app.config.js`).

## 🔧 Maintenance

Le fichier `index.html` est autonome et ne nécessite aucune dépendance externe. Toutes les ressources (CSS, JavaScript) sont inline pour garantir un chargement ultra-rapide.

## 📝 Notes

- GitHub Pages peut prendre quelques minutes pour déployer les changements
- Testez toujours avec un paramètre `token` pour simuler un vrai callback
- Les logs de la console sont utiles pour le debugging
