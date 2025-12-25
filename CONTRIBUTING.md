# 🤝 Guide de Contribution

Merci d'intéresser à Windows Cleaner ! Ce document explique comment contribuer correctement.

## 📋 Table des matières

- [Code de Conduite](#code-de-conduite)
- [Comment Contribuer](#comment-contribuer)
- [Processus de PR](#processus-de-pr)
- [Bonnes Pratiques](#bonnes-pratiques)

## 📜 Code de Conduite

Toute contribution doit respecter :
- Respecter les autres contributeurs
- Pas de langage offensant ou discriminatoire
- Créer un environnement inclusif

## 💡 Comment Contribuer

### 1. **Fork & Clone**
```bash
git clone https://github.com/YOUR-USERNAME/Windows-Cleaner.git
cd Windows-Cleaner
git remote add upstream https://github.com/christwadel65-ux/Windows-Cleaner.git
```

### 2. **Créer une Branche**
```bash
git checkout -b feature/ma-fonction
# ou
git checkout -b fix/mon-bug
```

### 3. **Faire des Commits Propres**
```bash
# Commits en français ou anglais, clairs et atomiques
git commit -m "feat: ajouter la fonction X"
git commit -m "fix: corriger le bug Y"
git commit -m "docs: améliorer README"
```

### 4. **Tester Localement**
```bash
dotnet build -c Release
dotnet test
```

### 5. **Pousser vers Votre Fork**
```bash
git push origin feature/ma-fonction
```

### 6. **Créer une Pull Request**
- Utilisez le template GitHub si disponible
- Décrivez **pourquoi** et **quoi**, pas juste **quoi**
- Liez les issues concernées : `Closes #123`
- Attendez 1+ approvals avant merge

## 🔄 Processus de PR

1. **Création** → GitHub Actions lance les tests
2. **Review** → Mainteneur(s) vérifie(nt) le code
3. **Feedback** → Répondez aux commentaires
4. **Approbation** → Si tout est bon, merge !

## ✅ Bonnes Pratiques

### Sécurité
- ✅ Ne commitez JAMAIS de secrets/clés API
- ✅ Ne commitez JAMAIS de credentials
- ✅ Testez vos changements avant de soumettre
- ✅ Signalez les bugs de sécurité via `SECURITY.md`

### Code
- ✅ Suivez le style C# du projet
- ✅ Documentez les nouvelles méthodes publiques
- ✅ Ajoutez des tests pour les nouvelles fonctionnalités
- ✅ Assurez-vous que `dotnet build` passe

### Documentation
- ✅ Mettez à jour le `README.md` si nécessaire
- ✅ Ajoutez des commentaires pour les logiques complexes
- ✅ Documentez les breaking changes dans `CHANGELOG.md`

### Commits
```
Format recommandé :

<type>(<scope>): <description>

[optionnel: body]

[optionnel: footer]

Types : feat, fix, docs, style, refactor, perf, test, chore, ci
Scope : Core, UI, Features, Docs, etc.
```

Exemple :
```
feat(Core): ajouter optimisation SSD

- Implémente TRIM pour disques SSD
- Ajoute vérification SMART
- Inclut tests unitaires

Closes #42
```

## 🐛 Signaler des Bugs

Utilisez les **GitHub Issues** avec :
1. Titre clair et concis
2. Étapes pour reproduire
3. Comportement attendu
4. Comportement réel
5. Votre système (Windows 10/11, version, specs)
6. Version de l'app

## 🎉 Améliorations Futures

Consultez le fichier `plans/IMPLEMENTATION_PLAN.md` pour les fonctionnalités prévues.

## ❓ Questions ?

- Consultez le `README.md`
- Ouvrez une discussion GitHub
- Vérifiez les issues existantes

---

**Merci pour votre contribution !** 🙌
