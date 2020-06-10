# Exercisi_USFlights
QueriesSQL


## Consultes 
/* Quantitat de registres de la taula de vols */

```
SELECT count(*) FROM `flights`
```

/*  Retard promig de sortida i arribada segons l’aeroport origen. */

/* Retard promig d’arribada dels vols, per mesos, anys i segons l’aeroport origen. A més, volen que els
resultat es mostrin de la següent forma (fixa’t en l’ordre de les files): */

```
LAX, 2000, 01, 10
LAX, 2000, 02, 30
LAX, 2000, 03, 2
…
LAX, 2000, 12, 4
LAX, 2001, 01, 5
…
LAX, 2001, 12, 4
ONT, 2000, 01, 6
ONT, 2000, 02, 3
```

/* Retard promig d’arribada dels vols, per mesos, anys i segons l’aeroport origen (mateixa consulta que abans  i amb el mateix ordre). Però a més, ara volen que en comptes del codi de l’aeroport es mostri el nom de la ciutat.*/

/* Les companyies amb més vols cancelats, per mesos i any. A més, han d’estar ordenades de forma que les companyies amb més cancel·lacions apareguin les primeres. */


/* L’identificador dels 10 avions que més distància han recorregut fent vols.*/

/* Companyies amb el seu retard promig només d’aquelles les quals els seus vols arriben al seu destí amb un retràs promig major de 10 minuts.*/


### Recursos
- [Flight DATA](http://stat-computing.org/dataexpo/2009/the-data.html)
- [STATISTICAL COMPUTING](http://stat-computing.org/)
- [SQL basics](https://www.w3schools.com/sql/sql_create_db.asp)


