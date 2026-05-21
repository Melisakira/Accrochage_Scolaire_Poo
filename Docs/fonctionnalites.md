# Fonctionnalités

## F1 - Gérer un élève

Créer, consulter et modifier le profil d'un élève.
Un élève possède un nom, un âge, un niveau scolaire et un score de risque calculé automatiquement.

## F2 - Enregistrer une absence

Saisir une absence pour un élève donné. 
Une absence est datée, le motif est renseigné, justifié ou non.
Chaque enregistrement déclenche une mise à jour du score de risque.

## F3 - Calculer le score de risque

Mise à jour automatique du score d'un élève selon le nombre d'absences injsutifiées et les signalements actifs. Le score détermine le profil de risque (faible/ moyen/ élevé).

## F4 - Déclencher une alerte

Quand le score franchit un seuil critique, une alerte est créée automatiquement et transmise à tous les intervenants abonnés à cet élève.
Pattern utilisé : Observer.

## F5 - Gérer les intervenants

Créer un intervenant (enseignant, éducateur, PMS) et l'assigner à un élève.
Un intervenant assigné devient automatiquement abonné aux alertes de cet élève.

## F6 - Ta	bleau de bord

Vue synthétique affichant :
- les élèves classés par niveau de risque
- les alertes actives non traitées
- les intervenants assignés par élève