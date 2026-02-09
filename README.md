# Pipeline ETL - Analyse de l'IA sur le Marché de l'Emploi Américain (2015-2025)

## 📋 Description du Projet

### Contexte
Analyse de l'évolution du marché de l'emploi américain sur 10 ans (2015-2025) pour comprendre l'impact de l'adoption massive de l'Intelligence Artificielle.

### Problématique
Comment l'adoption massive de l'Intelligence Artificielle influence-t-elle les salaires et la création d'entreprises dans les secteurs technologiques comparés aux secteurs traditionnels ?

### Données Sources
- Rapports trimestriels du Bureau of Labor Statistics (BLS)
- Période : 2015-2025
- Format initial : Excel (.xlsx)
- Conversion vers : Parquet pour performance

## 🎯 Objectifs Techniques

### Infrastructure
- **Plateforme** : Databricks avec Unity Catalog Volumes
- **Stockage** : Sécurisé et gouverné par Unity Catalog
- **Format** : Conversion Excel → Parquet (x10 vitesse)

### Traitement des Données
1. **Standardisation** : Conversion .xlsx → Parquet
2. **Consolidation** : Union des 4 fichiers trimestriels par année
3. **Nettoyage** : Agrégation avec `groupBy(ignorenulls=True)`
4. **Filtrage** : Suppression des lignes "Total"

## 📊 Indicateurs Clés de Performance (KPI)

| KPI | Description | Méthode de Calcul |
|-----|-------------|-------------------|
| **CAGR des Salaires** | Taux de croissance annuel moyen du salaire hebdomadaire avant/après 2022 | `(Valeur finale / Valeur initiale)^(1/n) - 1` |
| **Densité d'Entreprises** | Évolution du nombre d'établissements dans le secteur Tech (NAICS "Information") | `Σ(établissements_tech) / Σ(établissements_totaux)` |
| **Ratio de Richesse** | Écart de salaire Tech vs moyenne nationale | `Salaire_tech / Salaire_moyen_national` |
| **Complétude des Données** | Pourcentage de lignes avec 12 mois complets | `(Lignes_complètes / Lignes_totales) × 100` |

## 🔧 Architecture du Pipeline ETL

### Étape 1: Extraction
```python
# Lecture avec wildcard pour tous les fichiers
df = spark.read.parquet("*/*.parquet")
