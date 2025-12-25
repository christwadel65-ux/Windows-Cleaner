# 🔒 Politique de Sécurité

## Signalement des Vulnérabilités

Si vous découvrez une vulnérabilité de sécurité dans Windows Cleaner, **ne la publiez pas publiquement**. Au lieu de cela :

### 📧 Rapportez en Privé

1. **Email** : Contactez le mainteneur via une issue privée
2. **GitHub Security Advisory** : Utilisez la fonction de rapport privé sur GitHub
3. **Délai** : Donnez au mainteneur 90 jours pour corriger avant divulgation publique

### Informations à Inclure

- Description claire de la vulnérabilité
- Étapes pour la reproduire
- Impact potentiel
- Suggestions de correction (optionnel)

## Bonnes Pratiques de Sécurité

### Pour les Contributeurs

- ✅ Ne commitez JAMAIS de secrets, clés API, tokens, ou credentials
- ✅ Utilisez les GitHub Secrets pour les données sensibles
- ✅ Signez vos commits avec GPG quand possible (`git commit -S`)
- ✅ Testez les changements de sécurité avant de soumettre une PR

### Dépendances

- Maintenez régulièrement les dépendances NuGet à jour
- Utilisez Dependabot pour les alertes automatiques
- Vérifiez les vulnérabilités avec `dotnet list package --vulnerable`

### Code Review

- Tous les changements passent par une PR avec review
- Au moins 1 approbation avant merge
- Scans de sécurité (secrets, SAST) doivent passer

## Sécurité des Données

Windows Cleaner :
- ✅ N'envoie aucune donnée à distance
- ✅ Fonctionne entièrement hors ligne
- ✅ Peut être audité librement (code source public)
- ✅ Utilise uniquement les API Windows standard

## Disclaimer

Ce logiciel est fourni "tel quel" sans garantie. Les utilisateurs sont responsables des sauvegarde avant utilisation.

## Améliorations Futures

- [ ] Signature des releases avec GPG
- [ ] SBOM (Software Bill of Materials)
- [ ] Audit de sécurité externe
- [ ] CodeQL scanning automatique

---

**Dernière mise à jour** : 2025-12-25
