# Classes métier

## Domaine Événement 

### Evenement (abstraite)

Représente tout fait significatif pouvant influencer le score de risque d'un élève.
Classe abstraite - jamais instanciée directement.
- Attributs : date, description, poids
- Méthode abstraite : CalculerPoids()

### Absence
Spécialise Evenement.

Un élève peut être absent pour diverses raisons.
- Attributs : estJustifiee, motif
- Poids élevé si injustifiée
- Poids moyen si justifiée mais répétée

### Retard
Spécialise Evenement.

Un élève arrive après l'heure prévue.
- Attributs : dureeMinutes, estRepete
- Poids moyen, augmente si répété

### ResultatScolaire
Spécialise Evenement.

Un résultat isolé en dessous du seuil est un signal faible. C'est la répétition dans une même matière ou la multiplication sur plusieurs matières qui constitue un signal significatif.
- Attributs : matiere, note, seuilReussite
- Poids déterminé par la Strategy selon le contexte :
         - Faible si résultat isolé
         - Moyen si répété dans la même matière
         - Élevé si plusieurs matières simultanément

### Signalement
Spécialise Evenement.

Tout comportement ou situation préoccupante signalée par un membre de l'équipe éducative.
- Attributs : typeSignalement, gravite
- Poids variable selon gravité

## Domaine Élève

### Eleve

Représente un élève suivi par l'équipe éducative. C'est l'objet central de l'application.

- Attributs : nom, age, niveauScolaire, scoreRisque, evenements, profilRisque, intervenantsAbonnes, strategieCalcul
- Méthodes : EnregistrerEvenement(), CalculerScore(), AjouterIntervenant(), RetirerIntervenant(), Notifier()
- Implémente : IEvaluable
- Pattern Observer : intervenantsAbonnes, AjouterIntervenant(), RetirerIntervenant(), Notifier() - notifie automatiquement tous les intervenants abonnés quand le score franchit un seuil critique
- Pattern Strategy : strategieCalcul contient la logique de calcul du score. Ce pattern encapsule les trois angles d'analyse : temporalité, progression, combinaison.

La classe Eleve délègue le calcul sans connaître la logique interne.

### ProfilRisque (abstraite)

Représente le niveau de risque d'un élève.
Classe abstraite — jamais instanciée directement.
Chaque niveau spécialise le comportement à adopter quand le seuil est atteint.
- Méthode abstraite : EvaluerSeuil(int score)

### RisqueFaible
Spécialise ProfilRisque.

Élève stable, surveillance normale :
      - Score entre 0 et 30
      - Aucune alerte déclenchée

### RisqueMoyen
Spécialise ProfilRisque.

Élève nécessitant une vigilance accrue :
     - Score entre 31 et 60
     - Notification préventive aux intervenants

### RisqueEleve
Spécialise ProfilRisque.

Élève en situation critique :
    - Score supérieur à 60
    - Déclenche automatiquement une alerte

## Domaine Intervenant

### Intervenant (abstraite)

Représente tout professionnel pouvant intervenir auprès d'un élève à risque.
Classe abstraite — on n'instancie jamais un intervenant générique.
- Attributs : nom, prenom, contact
- Méthode abstraite : Intervenir(Eleve eleve)
- Implémente : INotifiable
- Pattern Observer : reçoit les notifications envoyées par Eleve via INotifiable

### IntervenantInterne (abstraite)
Spécialise Intervenant.

Représente tout professionnel travaillant au sein de l'établissement scolaire.
- Attribut : etablissement

### Direction
Spécialise IntervenantInterne.

Prend les décisions administratives et disciplinaires.
- Intervenir() : décision administrative, convocation, signalement officiel

### EnseignantTitulaire
Spécialise IntervenantInterne.

Premier contact pédagogique de l'élève. Détecte les signaux faibles au quotidien.
- Attribut : classeTitle
- Intervenir() : contact pédagogique direct, entretien individuel, contact famille

### Educateur
Spécialise IntervenantInterne.

Accompagne l'élève dans son quotidien scolaire et para-scolaire.
- Intervenir() : accompagnement socio-éducatif, médiation, soutien quotidien

### ConseillerPMS
Spécialise IntervenantInterne.

Oriente l'élève dans son parcours scolaire et professionnel.
- Intervenir() : guidance scolaire, bilan d'orientation, entretien

### PsychologuePMS
Spécialise IntervenantInterne.

Assure le suivi psychologique de l'élève.
- Intervenir() : suivi psychologique,
  évaluation, soutien émotionnel

### AssistantSocialPMS
Spécialise IntervenantInterne.

Intervient sur les aspects sociaux et familiaux de la situation.
- Intervenir() : accompagnement social, lien avec la famille, accès aux droits

### IntervenantExterne (abstraite)
Spécialise Intervenant.

Représente tout professionnel extérieur à l'établissement scolaire. 
- Attribut : organisation

### EducateurRue
Spécialise IntervenantExterne.

Intervient hors cadre scolaire, dans le milieu de vie de l'élève.
- Intervenir() : accompagnement de rue, lien social, prévention

### ServiceExterne
Spécialise IntervenantExterne.

Représente un service spécialisé externe comme le CPAS, le SAS, l'AMO...
- Attributs : nomService, typeService
- Intervenir() : orientation vers service spécialisé, prise en charge

## Domaine Suivi

### Suivi

Représente le suivi actif d'un élève par un intervenant sur une période donnée.
Un suivi regroupe toutes les actions mises en place pour un élève.
- Attributs : dateDebut, statut, objectif, eleve, intervenant, actionsRealisees
- Statuts possibles : en cours, suspendu, clôturé

### Action

Représente une action concrète mise en place dans le cadre d'un suivi.
- Attributs : date, description, typeAction, resultat
- Types possibles : entretien, contact famille, réunion PMS, orientation, médiation

### Alerte

Représente une notification créée automatiquement quand le score d'un élève franchit le seuil critique.
Transmise à tous les intervenants abonnés à cet élève.
- Attributs : dateCreation, niveau, message, estTraitee