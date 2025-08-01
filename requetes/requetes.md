## Requêtes du Projet

## 1) Lister les numéros de contrats (contrat_ID) avec leur surface pour la commune de Caen
```sql
SELECT contrat_ID, Surface
FROM contrat
WHERE commune = "CAEN";
```

## 2) Lister les numéros de contrat avec le type de contrat et leur formule pour les maisons du département de la Saône-et-Loire (Département 71)
```sql
SELECT contrat_ID, formule
FROM contrat
WHERE type_local = "Maison"
AND code_departement = "71";
```

## 3) Lister le nom des régions de France
```sql
SELECT DISTINCT reg_nom
FROM region;
```

## 4) Combien existe-t-il de contrats sur les résidences principales ?
```sql
SELECT COUNT(DISTINCT contrat_ID) AS nb_contrats_rp
FROM contrat
WHERE type_contrat = "Residence principale";
```

## 5) Quelle est la surface moyenne des logements avec un contrat à Paris 
```sql
SELECT AVG(surface) AS moyenne_surface_paris
FROM contrat
WHERE commune LIKE "PARIS%";  ## On aurait aussi pu filtrer avec WHERE code_departement = '75'
```

## 6) Quels sont les 5 contrats avec les surfaces les plus élevées ?
```sql
SELECT contrat_ID, surface
FROM contrat
ORDER BY surface DESC
LIMIT 5;
```

## 7) Quel est le prix moyen de la cotisation mensuelle ?
```sql
SELECT AVG(prix_cotisation_mensuel) AS cotisation_moyenne
FROM contrat;
```

## 8) Quel est le nombre de contrats pour chaque catégories de prix de la valeur déclarée des biens ?
```sql
SELECT valeur_declaree_biens, COUNT(DISTINCT contrat_ID) AS nb_contrats_valeur
FROM contrat
GROUP BY valeur_declaree_biens;
```

## 9) Quels sont les 10 départements où le prix moyen de la cotisation est le plus élevé ?
```sql
SELECT r.dep_nom, r.dep_code, AVG(c.prix_cotisation_mensuel) AS moyenne_prix_dpt
FROM contrat c 
JOIN region r ON c.code_postal = r.code_postal
GROUP BY r.dep_nom, r.dep_code
ORDER BY moyenne_prix_dpt DESC
LIMIT 10;
```

## 10) Quel est le nombre de contrats avec des formules "Integral" pour la région Pays de la Loire ?
```sql
SELECT COUNT(DISTINCT c.contrat_ID) AS nb_contrats_integral_pdl
FROM contrat c
JOIN region r ON c.code_postal = r.code_postal
WHERE c.formule = "Integral"
AND r.reg_nom = "Pays de la Loire";
```

## 11) Liste des communes ayant eu au moins 150 contrats ?
```sql
SELECT commune, COUNT(DISTINCT contrat_ID) AS nb_contrats_uniques
FROM contrat
GROUP BY commune
HAVING nb_contrats_uniques >= 150;
```

## 12) Quel est le nombre de contrats pour chaque région ?
```sql
SELECT r.reg_nom, COUNT(DISTINCT c.contrat_ID) AS nb_contrats_regions
FROM contrat c
JOIN region r ON c.code_postal = r.code_postal
GROUP BY r.reg_nom;
```
