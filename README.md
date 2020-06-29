# Exercisi_USFlights
QueriesSQL

## tools used:
[XAMPP](https://www.apachefriends.org/es/index.html)(Apache, PhpMyAdmin) with DB files in .sql and imported data from .csv. 

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
Any other way will not work for important data are missing in flight table and connections between .csv files. First you need to add the connections between the datatables in the different files (index, add Primary Key, add Foreign Key) and add the missing colums in flightdb.

b. During the data import from flights table, are the fields in the csv file from which they are imported well correlated with the fields in the table? Why do you think this is?

No, the datafields in the .csv file do NOT well correlate with the datafield in the table(db). As you can observe in the data [Flight DATA](http://stat-computing.org/dataexpo/2009/the-data.html), the last 5 columns are missing. And in the datatable "flights" the column 
"flightID" is missing. 

To solve this:
- Create a first column "flightID" with PRIMARY KEY AUTOINCREMENT. After this you can import table.
- After import, add 5 new (missing) columns in datatable "flights": CarrierDelay,WeatherDelay,NASDelay,SecurityDelay,LateAircraftDelay

### Consultes (exercise SQL queries):
5) Include all queries in a .sql file and add them to your github repository:

/* SQL CONSULTA 1: Quantitat de registres de la taula de vols */
```
SELECT COUNT(*) FROM `flights`
```
ANSWER: 
COUNT(*)
4758

REFLECTION:
- The first SQL query leads to 361 flights. It seems in the flightdb many flights are missing.
- It is solved now. I did not import the flights db correctly. 
To solve: I emptied the flights table with TRUNCATE and imported flights.csv anew. This time with the correct "Format-specific options.
![Format-specific options Flightsdb](https://github.com/dianavile/Exercisi_USFlights/blob/master/importFLIGHTS.PNG)
Before doing so, I checked all columns in DB carriersdb, usairportsdb and flightsdb with .csv file for typos and made some small changes. After this, the database was imported correctly.
   
/* SQL CONSULTA 2:  Retard promig de sortida i arribada segons l’aeroport origen. */
```
SELECT `Origin` AS "Origen", 
AVG(`ArrDelay`) AS "prom_arribades", 
AVG(`DepDelay`) AS "prom_sortides" 
FROM `flights` 
GROUP BY Origin
```
ANSWER: lo mismo cómo el ejercicio.

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
```
SELECT `Origin`,`colYear`,`colMonth`, 
AVG(`ArrDelay`) AS "prom_arribades" 
FROM `flights` 
GROUP BY Origin, colYear, colMonth;
```
ANSWER: lo mismo cómo el ejercicio.

/* SQL CONSULTA 4: Retard promig d’arribada dels vols, per mesos, anys i segons l’aeroport origen (mateixa consulta que abans  i amb el mateix ordre). Però a més, ara volen que en comptes del codi de l’aeroport es mostri el nom de la ciutat.*/
```
SELECT `city`,`colYear`,`colMonth`, 
AVG(`ArrDelay`) AS "prom_arribades" 
FROM `flights`, `usairports` 
WHERE Origin = iata 
GROUP BY city, colYear, colMonth;
```
ANSWER: lo mismo cómo el ejercicio.

/* SQL CONSULTA 5: Les companyies amb més vols cancelats, per mesos i any. A més, han d’estar ordenades de forma que les companyies amb més cancel·lacions apareguin les primeres. */
```
SELECT `UniqueCarrier`, `colYear`, `colMonth`, 
SUM(`Cancelled`) AS "total_cancelled" 
FROM `flights` 
GROUP BY `colYear`, `colMonth`, `UniqueCarrier` 
HAVING SUM(`Cancelled`) > 0
ORDER BY `total_cancelled` DESC
```
ANSWER: lo mismo cómo el ejercicio.

/* SQL CONSULTA 6: L’identificador dels 10 avions que més distància han recorregut fent vols.*/
```
SELECT `TailNum`, SUM(`Distance`) AS "total_distance" 
FROM `flights` 
WHERE `TailNum` <> "" 
GROUP BY `TailNum` 
ORDER BY `total_distance` DESC
LIMIT 10;
```
ANSWER: lo mismo cómo el ejercicio.

/* SQL CONSULTA 7: Companyies amb el seu retard promig només d’aquelles les quals els seus vols arriben al seu destí amb un retràs promig major de 10 minuts.*/
```
SELECT `UniqueCarrier`, AVG(`ArrDelay`) AS "avg_delay" 
FROM `flights` GROUP 
BY `UniqueCarrier` 
HAVING AVG(`ArrDelay`) > 10 
ORDER BY `avg_delay` DESC;
```
ANSWER: No cuadra. probablemente, porque en este SQL query 10 minutos de retraso no esta incluido. 
Tiene que ser un retraso promedio de MAS de 10 minutos. Yo hizo de 10 minutos. 

SQL CONSULTA 7-1
```
SELECT `UniqueCarrier`, AVG(`ArrDelay`) 
AS "avg_delay" 
FROM `flights` 
GROUP BY `UniqueCarrier` 
HAVING AVG(`ArrDelay`) > 11
ORDER BY `avg_delay` DESC; 
```
SQL CONSULTA 7-2
```
SELECT `UniqueCarrier`, AVG(`ArrDelay`) 
AS "avg_delay" 
FROM `flights` 
GROUP BY `UniqueCarrier` 
HAVING AVG(`ArrDelay`) > 10 
ORDER BY `avg_delay` DESC 
LIMIT 10;
```
ANSWER: Todavia no cuadra. He probado 2 variantes (SQL CONSULTA 7-1 y SQL CONSULTA 7-2), pero sigo teniendo un error en dos columnas. 
Adjunto imagen.
![SQL CONSULTA 7](https://github.com/dianavile/Exercisi_USFlights/blob/master/SQL%20query7-2ndIntent.PNG)


## correction USFLIGHT:
- Consulta 1 i 2, perfecte

- Consulta 3: Faltaria definir ordre: 
```ORDER BY Origin, colYear, colMonth;```

- Consulta 4: Cuando consultas campos del mismo nombre en tablas diferentes, deberías utilizar un identificativo. 
Mira este ejemplo, que además utiliza el Left JOIN:
```SELECT AIRP.City, FL.colYear, FL.colMonth, AVG(FL.ArrDelay) 
FROM Flights as FL 
LEFT JOIN USAirports as AIRP  
ON FL.Origin = AIRP.IATA 
GROUP BY City, colYear, colMonth  
ORDER BY City, colYear, colMonth; (no és obligatori ordenar)
```

- Consulta 5: Cuando especificas SUM (‘Cancelled’) as ‘identificador’, ese identificador ya lo puedes utilizar en el Having sum, no tiene sentido que lo vuelvas a crear:
```HAVING total_cancelacions > 0```

- Consulta 6: Perfect!

- Consulta 7: Lo mismo que la consulta 5 ->
```HAVING AVG(`ArrDelay`) > 10```
- lo correcto sería ``HAVING avg_delay > 10````
Esta sería la consulta completa:
```
SELECT UniqueCarrier, avg(ArrDelay) as avgDelay 
	FROM Flights 
	GROUP BY UniqueCarrier 
	HAVING avgDelay > 10.0 
	ORDER BY avgDelay DESC;``
   
### Recursos
- [SQLBolt-Introduction to SQL](https://sqlbolt.com/)
- [SQL basics](https://www.w3schools.com/sql/sql_create_db.asp)
