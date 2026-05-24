# Design Pattern — Observer

## Problème identifié

Quand le score de risque d'un élève franchit un seuil critique, plusieurs professionnels doivent être notifiés — mais pas toujours les mêmes, et chacun réagit de façon indépendante selon son rôle. 

Chaque élève a un profil unique : problèmes familiaux, difficultés scolaires, comportement perturbateur - ou une combinaison de ces facteurs. L'équipe d'intervenants est donc constituée au cas par cas, qu'il s'agisse de professionnels internes à l'établissement ou d'intervenants extérieurs comme les équipes mobiles, le SAS, le CPAS ou l'AMO. 

Sans pattern, 'Eleve' devrait connaître chaque intervenant individuellement, savoir qui appeler et comment. Couplage fort, le code deviendrait fragile, difficile à faire évoluer, et ne refléterait pas la réalité du terrain où les équipes varient selon les élèves et les situations.

## Solution — Pattern Observer

### Participants dans le projet

| Rôle pattern | Classe projet |
|---|---|
| Sujet | Eleve |
| Observateur | INotifiable |
| Observateur concret | Direction, EnseignantTitulaire, Educateur, ConseillerPMS, PsychologuePMS, AssistantSocialPMS, EducateurRue, ServiceExterne |
| Notifier() | Eleve.Notifier() |
| Abonner() | Eleve.AjouterIntervenant() |
| Désabonner() | Eleve.RetirerIntervenant() |

### Fonctionnement

1. L'intervenant responsable assigne un intervenant à un élève via Ajouter un intervenant — cette assignation constitue automatiquement un abonnement
2. Quand Calculer le score franchit le seuil de vigilance (31-60), Notifier() envoie une notification préventive à tous les intervenants abonnés
3. Quand Calculer le score franchit le seuil critique (supérieur à 60), Notifier() déclenche une alerte automatique à tous les intervenants abonnés
4. Chaque intervenant reçoit l'alerte et réagit de façon indépendante selon son rôle propre
5. Un intervenant peut être désabonné si son suivi de l'élève prend fin
6. Les élèves dont le score approche le seuil sans l'avoir franchi sont visibles dans le tableau de bord — l'intervenant responsable peut agir de façon manuelle et proactive

## Justification

Sur le terrain éducatif, la communication entre intervenants est l'un des principaux obstacles à la prévention du décrochage. Les intervenants internes ne se connaissent pas toujours entre eux, et encore moins les intervenants externes. Chacun agit dans son couloir, sans vision globale de la situation de l'élève.
Sans coordination, les actions se superposent, se contredisent ou n'arrivent tout simplement pas. Le jeune se retrouve sans information sur ce qui se passe autour de lui, sans action cohérente, jusqu'au décrochage, au renvoi ou à l'absence totale de suivi.
Le pattern Observer répond directement à cette réalité : chaque intervenant est notifié selon son rôle, de façon indépendante, sans avoir besoin de connaître les autres. 'Eleve' ne sait pas qui compose l'équipe - il notifie, et chacun réagit selon sa propre responsabilité. Par ailleurs, au-delà de l'aspect technique, ce pattern porte aussi une dimension éthique. Chaque intervenant est notifié selon son rôle — il reçoit l'information qui le concerne, pas l'ensemble du dossier de l'élève. Cela reflète le principe du secret partagé en vigueur dans le secteur éducatif et de l'aide à la jeunesse en Belgique : chaque professionnel partage uniquement ce que son rôle et la loi lui permettent de partager.
C'est la traduction informatique d'un protocole d'alerte qui devrait exister sur le terrain mais qui, faute d'outil, reste trop souvent informel et aléatoire.