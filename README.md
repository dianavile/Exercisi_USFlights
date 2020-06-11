# Exercisi_USFlights
QueriesSQL

## tools used:
XAMPP (Apache), PhpMyAdmin (DB,SQL queries,.CSV)

### Installation:
- Install Xampp (for Windows)
- Download the Zip files (exercise)

### exercise DB:
1) Start a connection with the root user and mysql password
2) Create Database (DB) with the necessary tables (see:createUSFlightsSchema script in Zip).
3) Import data.*
### DATA 
- [Flight DATA](http://stat-computing.org/dataexpo/2009/the-data.html)
- [STATISTICAL COMPUTING](http://stat-computing.org/)

### REFLECTION:
a. In what order should the data be imported?

The data should be imported in the following way: carriers.csv, airports.csv, flights.csv
Any other way will not work for important data are missing.

b. During the data import from flights table, are the fields in the csv file from which they are imported well correlated with the fields in the table? Why do you think this is?

No, the datafields in the .csv file do not well correlate with the datafield in the table(db). As you can observe in the data [Flight DATA](http://stat-computing.org/dataexpo/2009/the-data.html), the last 5 columns are missing. And in the datatable "flights" the column 
"flightID" is missing.

To solve this:
- Create a first column "flightID" with PRIMARY KEY AUTOINCREMENT. After this you can import table.
- After import, add 5 new (missing) columns in datatable "flights": CarrierDelay,WeatherDelay,NASDelay,SecurityDelay,LateAircraftDelay

### Consultes (exercise SQL queries):
5) Include all queries in a .sql file and add them to your github repository:

/* SQL CONSULTA 1: Quantitat de registres de la taula de vols */
```
SELECT count(*) FROM `flights`
```
/* SQL CONSULTA 2:  Retard promig de sortida i arribada segons l’aeroport origen. */
```

```
/* SQL CONSULTA 3: Retard promig d’arribada dels vols, per mesos, anys i segons l’aeroport origen. A més, volen que els
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

/* SQL CONSULTA 4: Retard promig d’arribada dels vols, per mesos, anys i segons l’aeroport origen (mateixa consulta que abans  i amb el mateix ordre). Però a més, ara volen que en comptes del codi de l’aeroport es mostri el nom de la ciutat.*/
```

```
/* SQL CONSULTA 5: Les companyies amb més vols cancelats, per mesos i any. A més, han d’estar ordenades de forma que les companyies amb més cancel·lacions apareguin les primeres. */
```

```

/* SQL CONSULTA 6: L’identificador dels 10 avions que més distància han recorregut fent vols.*/
```

```

/* SQL CONSULTA 7: Companyies amb el seu retard promig només d’aquelles les quals els seus vols arriben al seu destí amb un retràs promig major de 10 minuts.*/
```

```

### Recursos
- [SQLBolt-Introduction to SQL](https://sqlbolt.com/)
- [SQL basics](https://www.w3schools.com/sql/sql_create_db.asp)
