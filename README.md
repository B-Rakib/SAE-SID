I. Présentation du projet

Contexte
Les réseaux sociaux représentent une ressource précieuse pour analyser et comprendre les comportements des utilisateurs en ligne. Ce projet vise à explorer les tendances globales des interactions, les sentiments exprimés, et leur impact sur les dynamiques sociales à travers des données structurées.

Problématique
Comment exploiter les données des réseaux sociaux pour comprendre les comportements des utilisateurs et les tendances globales d'engagement en ligne ?

Objectifs
Fournir une vision complète des comportements sur les réseaux sociaux en exploitant des données fiables.
Identifier les tendances clés, telles que les types d'interactions et les sentiments dominants.
Présenter des résultats à l'aide de tableaux de bord interactifs dans Power BI.
Auteurs : Riade El Attar, Rakib Bhuiyan

II. Modélisation du SID
Choix du processus métier à modéliser
L’analyse se concentrera sur les éléments suivants :

Les types d'interactions sur les réseaux sociaux (likes, partages, commentaires).
Les sentiments exprimés par les utilisateurs.
Les tendances d'engagement globales.
Définition de la granularité
Chaque ligne de la table de faits représentera une interaction utilisateur, avec les détails suivants :

Le sentiment exprimé.
Le type d'interaction (like, commentaire, partage).
Les informations sur l'utilisateur et la plateforme concernée.
Choix des dimensions
dim_users : Informations sur les utilisateurs (ID utilisateur, âge, genre, localisation).
dim_platforms : Plateformes de réseaux sociaux (Twitter, Facebook, Instagram, etc.).
dim_interactions : Types d'interaction (like, partage, commentaire).
dim_time : Une table calendrier pour les analyses temporelles.
Identification des faits (Mesures)
Les mesures principales incluront :

Le nombre total d'interactions.
Le score moyen de sentiment (positif, neutre, négatif).
Le nombre d'interactions par plateforme et par type.
III. Intégration de données (Processus ETL)
1. Extraction des données
Sources utilisées :

social_media_usage.csv : Contient les types d'interactions.
sentimentdataset.csv : Données sur les sentiments liés aux publications.
data1.csv et Base_de_donnees (1).xlsx : Métadonnées supplémentaires sur les utilisateurs.
Étapes :

Importer les données dans Power BI via Obtenir des données > Texte/CSV ou Excel.
Centraliser les données sur un dépôt commun pour garantir la collaboration.
2. Transformation des données
Suppression des colonnes non pertinentes : Éliminer les colonnes inutiles (ex. : identifiants temporaires, métadonnées non exploitables).
Gestion des doublons et erreurs :
Supprimer les doublons.
Remplacer les valeurs manquantes par des valeurs par défaut ou des moyennes (selon les cas).
Création de colonnes personnalisées :
Une colonne de score de sentiment, attribuant des valeurs numériques aux sentiments : positif = 1, neutre = 0, négatif = -1.
Catégorisation des âges en groupes (ex. : <18, 18-25, 26-35).
Uniformisation des formats :
Conversion des dates au format européen (DD/MM/YYYY).
Harmonisation des noms des plateformes.
3. Création et utilisation de tables de temps
Créer une table calendrier avec DAX dans Power BI :

DAX
Copier
Modifier
CalendarTable = ADDCOLUMNS(
    CALENDAR(DATE(2020, 1, 1), DATE(2025, 12, 31)),
    "Year", YEAR([Date]),
    "Month", MONTH([Date]),
    "Weekday", FORMAT([Date], "dddd"),
    "Quarter", QUARTER([Date])
)

IV. Description des modèles de données
Modèle en étoile
Le modèle utilisé sera en étoile pour sa simplicité et son adaptabilité aux analyses multidimensionnelles.

Table centrale (faits) :

Contiendra des mesures comme le nombre total d'interactions, le score moyen des sentiments, et les volumes d'interactions par type.
Tables dimensionnelles :

dim_users : Contiendra des détails démographiques et géographiques des utilisateurs.
dim_platforms : Répertorie les plateformes de réseaux sociaux.
dim_interactions : Décrit les types d'interactions (like, commentaire, partage).
dim_time : Fournira une vue temporelle des données.
V. Restitution et Tableaux de bord
Reporting dans Power BI
Les analyses incluront :

Interactions par plateforme :
Histogrammes des interactions (likes, partages, commentaires).
Carte interactive pour analyser les interactions par localisation.
Analyse des sentiments :
Diagramme circulaire pour visualiser les proportions de sentiments exprimés (positif, neutre, négatif).
Courbes temporelles des tendances de sentiments par plateforme.
Analyse des tendances des utilisateurs :
Répartition des interactions par tranche d'âge et localisation.
Classement des utilisateurs les plus actifs (Top 10).
Engagement global :
Visualisation de l'évolution temporelle des interactions.
Étapes supplémentaires
GitHub :
Créer un dépôt structuré avec des dossiers pour :
Les fichiers bruts de données.
Le rapport final.
Les fichiers Power BI.
Ajouter le collaborateur avec l’adresse email fournie.
Soutenance :
Préparer une présentation synthétique de 5 minutes avec :
Contexte, problématique, et objectifs.
Étapes d’intégration des données.
Démonstration des tableaux de bord interactifs.
