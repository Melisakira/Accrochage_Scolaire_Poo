# Interfaces

## INotifiable

Contrat implémenté par tout objet pouvant recevoir une alerte.
Implémentée par : Direction, EnseignantTitulaire, Educateur, ConseillerPMS, PsychologuePMS, AssistantSocialPMS, EducateurRue, ServiceExterne
- En risque faible : notification déclenchée manuellement par l'intervenant responsable
- En risque moyen et élevé : notification déclenchée automatiquement

```csharp
interface INotifiable
{
    void RecevoirAlerte(Alerte alerte);
}
```

## IEvaluable

Contrat implémenté par tout objet dont on peut calculer un score.
Implémentée par : Eleve

```csharp
interface IEvaluable
{
    int CalculerScore();
}
```

## IStrategieCalcul

Contrat implémenté par toute stratégie de calcul du score de risque.
Implémentée par : StrategieTemporalite, StrategieProgression, StrategieCombinaison

```csharp
interface IStrategieCalcul
{
    int Calculer(List<Evenement> evenements);
}
```