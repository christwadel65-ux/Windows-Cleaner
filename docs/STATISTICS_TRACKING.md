# Suivi des Statistiques - Windows Cleaner v1.0.6

## Vue d'ensemble

Windows Cleaner v1.0.6 enregistre automatiquement des statistiques détaillées sur chaque session de nettoyage. Ces statistiques incluent maintenant le suivi complet des caches applicatifs et de l'optimisation SSD.

## Statistiques Enregistrées

### Informations de Base
- **Timestamp** : Date et heure du nettoyage
- **ProfileUsed** : Nom du profil de nettoyage utilisé
- **FilesDeleted** : Nombre total de fichiers supprimés
- **BytesFreed** : Nombre total d'octets libérés
- **Duration** : Durée totale de la session
- **WasDryRun** : Indique si c'était une simulation (dry-run)

### Statistiques des Caches Applicatifs (Nouveau 1.0.6)

Les statistiques suivantes sont enregistrées pour chaque type de cache d'application:

#### Compteurs Individuels
- **VsCodeCacheFilesDeleted** : Nombre de fichiers VS Code cache supprimés
- **NugetCacheFilesDeleted** : Nombre de fichiers NuGet cache supprimés
- **MavenCacheFilesDeleted** : Nombre de fichiers Maven cache supprimés
- **NpmCacheFilesDeleted** : Nombre de fichiers npm cache supprimés
- **GameCachesFilesDeleted** : Nombre de fichiers jeux (Steam/Epic) supprimés

#### Métriques Agrégées
- **AppCachesBytesFreed** : Total d'octets libérés par les caches applicatifs
- **TotalCachesDeleted** : Somme de tous les fichiers app cache supprimés (propriété calculée)
- **FormattedAppCachesSize** : Affichage formaté en B/KB/MB/GB (propriété calculée)

### Statistiques d'Optimisation SSD (Nouveau 1.0.6)

- **SsdOptimized** : Indique si l'optimisation TRIM a été effectuée
- **DiskHealthChecked** : Indique si une vérification SMART a été effectuée
- **DiskHealthReport** : Rapport détaillé de l'état SMART du disque

## Rapport HTML Généré

Le rapport HTML généré contient les sections suivantes:

### 1. Résumé Global
- Affichage en cartes colorées des statistiques globales
- Total de fichiers supprimés (tous les nettoyages)
- Espace total libéré (tous les nettoyages)
- Nombre de sessions exécutées
- Moyenne de fichiers supprimés par session

### 2. Statistiques des 30 Derniers Jours
- Espace libéré sur 30 jours
- Fichiers supprimés sur 30 jours
- Nombre de nettoyages sur 30 jours

### 3. Nettoyage des Caches Applicatifs
- **Statistiques Globales** : Total fichiers app cache + total espace libéré
- **Détail par Source** : Breakdown par VS Code, NuGet, Maven, npm, Jeux

### 4. Optimisation SSD
- Nombre de sessions TRIM effectuées
- Nombre de vérifications SMART effectuées
- Dernier rapport SMART (si disponible)

### 5. Historique des Sessions
Tableau affichant les 50 dernières sessions avec:
- Date et heure
- Profil utilisé
- Nombre de fichiers supprimés
- Espace libéré
- Indicateur d'app cache (✓ + comptage)
- Indicateur SSD (✓ si optimisé)
- Durée de la session

## Intégration dans RunCleanup()

Les statistiques sont enregistrées automatiquement lors de chaque exécution:

```csharp
// Dans Program.cs et MainForm.cs
if (!dryRun)
{
    StatisticsManager.RecordCleaningSession(new CleaningStatistics
    {
        ProfileUsed = profile.Name,
        FilesDeleted = result.FilesDeleted,
        BytesFreed = result.BytesFreed,
        Duration = duration,
        
        // App cache stats
        VsCodeCacheFilesDeleted = result.VsCodeCacheFilesDeleted,
        NugetCacheFilesDeleted = result.NugetCacheFilesDeleted,
        MavenCacheFilesDeleted = result.MavenCacheFilesDeleted,
        NpmCacheFilesDeleted = result.NpmCacheFilesDeleted,
        GameCachesFilesDeleted = result.GameCachesFilesDeleted,
        AppCachesBytesFreed = result.AppCachesBytesFreed,
        
        // SSD stats
        SsdOptimized = result.SsdOptimized,
        DiskHealthChecked = result.DiskHealthChecked,
        DiskHealthReport = result.DiskHealthReport
    });
}
```

## Stockage des Données

Les statistiques sont stockées en JSON dans:
```
%APPDATA%\WindowsCleaner\statistics.json
```

Format de chaque entrée:
```json
{
    "Timestamp": "2025-01-15T14:32:00",
    "ProfileUsed": "Complet",
    "FilesDeleted": 1250,
    "BytesFreed": 5368709120,
    "VsCodeCacheFilesDeleted": 45,
    "NugetCacheFilesDeleted": 120,
    "MavenCacheFilesDeleted": 15,
    "NpmCacheFilesDeleted": 32,
    "GameCachesFilesDeleted": 8,
    "AppCachesBytesFreed": 1024000000,
    "SsdOptimized": true,
    "DiskHealthChecked": true,
    "DiskHealthReport": "[SMART Health Report]...",
    "Duration": "00:01:23.456",
    "WasDryRun": false
}
```

## Accès aux Statistiques

### Via CLI
```bash
windows-cleaner.exe --export-report
```
Exporte un rapport HTML sur le Bureau

### Via Code
```csharp
// Charger toutes les statistiques
var allStats = StatisticsManager.LoadAllStatistics();

// Récupérer les 30 derniers jours
var last30Days = StatisticsManager.GetRecentStatistics(30);

// Obtenir les totaux
int totalFiles = StatisticsManager.GetTotalFilesDeleted();
long totalBytes = StatisticsManager.GetTotalBytesFreed();
int totalSessions = StatisticsManager.GetTotalSessions();

// Générer et exporter le rapport HTML
string reportPath = StatisticsManager.ExportHtmlReport();

// Effacer toutes les statistiques
StatisticsManager.ClearAllStatistics();
```

## Bénéfices pour l'Utilisateur

1. **Visibilité Complète** : Voir exactement ce qui a été nettoyé et où
2. **Analyse Détaillée** : Comprendre quels caches consomment le plus d'espace
3. **Historique Long Terme** : Suivre l'accumulation de fichiers temporaires au fil du temps
4. **Santé Système** : Monitorer l'état du SSD avec les rapports SMART
5. **Statistiques Personnalisées** : Comparer les résultats entre différents profils de nettoyage

## Amélioration Continue

Les statistiques permettent d'identifier:
- Les caches applicatifs qui accumulent le plus de fichiers
- Les patterns de nettoyage efficaces
- Les problèmes potentiels de santé disque (via SMART)
- Les améliorations à apporter aux profils de nettoyage
