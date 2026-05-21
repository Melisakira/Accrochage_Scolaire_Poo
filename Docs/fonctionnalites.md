# Fonctionnalités

## F1 - Gérer un élève

Créer, consulter et modifier le profil d'un élève.
Un élève possède un nom, un âge, un niveau scolaire et un score de risque calculé automatiquement à partir des ses événements.

## F2 - Enregistrer un évènement

Saisir tout événement significatif pour un élève : 
- Absence justifiée ou non
- Retard répété
- Résultat scolaire insuffisant
- Signalement comportemental ou social.

Chaque événement a un poids dans le calcul du score de risque et déclenche une mise à jour automatiquement.

## F3 - Calculer le score de risque

Mise à jour automatique du score d'un élève selon l'ensemble des événements enregistrés.

Chaque type d'événement a un poids différent :
- Absence injustifiée : poids élevé
- Absence justifiée répétée : poids moyen
- Retard mutiple : poids moyen
- Signalement : poids variable selon la gravité

Le score détermine le profil de risque (faible/ moyen/ élevé).

## F4 - Assigner un intervenant à un élève

Céer un intevervenant (direction de l'établissement, enseignant titularisé, PMS ou externe) et l'assigner à un élève.
L'assignation constitue un abonnement : l'intervenant sera automatiquement notifié lors de chaque alerte concernant cet élève. Il est également possible de désassigner un intervenant.

## F5 - Déclencher une alerte

Quand le score franchit un seuil critique, une alerte est créée automatiquement et transmise à tous les intervenants abonnés à cet élève.

Pattern utilisé : Observer. Chaque intervenant reçoit l'alerte et réagit selon son rôle propre.

## F6 - Enregistrer une action de suivi

Documenter chaque action mise en place pour un élève :
- Type d'action (entretien, orientation, contact famille, réunion PMS ...)
- Date et description
- Résultat observé

Un suivi regroupe l'ensemble des actions réalisées pour un élève par un ou plusieurs intervenant.s.

## F6 - Tableau de bord

Vue synthétique affichant :
- les élèves classés par niveau de risque
- les alertes actives non traitées
- les intervenants assignés par élève
- les dernières actions réalisées par élève
- le statut du suivi avtif et clôturé