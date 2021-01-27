# afu_ipw_bauzonen

## Requirements

- PostGIS > 3.x (GEOS...)


## Datenbank

```
docker-compose up
```

Die Daten bleiben auch z.B. nach `docker-compose stop` oder `docker-compose down` erhalten. Falls man mit leeren DBs neu starten möchte:

```
docker-compose down
docker volume prune
```

Credentials: 

* Hostname: `localhost`
* Port: `54321`
* DB-Name: `edit`
* Benutzer: `gretl` (für Lese- und Schreibzugriff) oder `admin` (zum Anlegen von Schemen, Tabellen usw.); das Passwort lautet jeweils gleich wie der Benutzername

## Modell anlegen

```
java -jar /Users/stefan/apps/ili2pg-4.4.4/ili2pg-4.4.4.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr admin --dbpwd admin --dbschema arp_bauzonengrenzen_pub --createEnumTabs --strokeArcs --defaultSrsCode 2056 --nameByTopic --models SO_ARP_Bauzonengrenzen_20210120 --modeldir "./model/;http://models.geo.admin.ch" --schemaimport
```

## Nutzungplanung (Pub) importieren

```
java -jar /Users/stefan/apps/ili2pg-4.4.4/ili2pg-4.4.4.jar --dbhost localhost --dbport 54322 --dbdatabase pub --dbusr admin --dbpwd admin --dbschema arp_npl_pub --disableValidation --strokeArcs --defaultSrsCode 2056 --nameByTopic --models SO_Nutzungsplanung_Publikation_20190909  --doSchemaImport  --import /Users/stefan/Downloads/ch.so.arp.nutzungsplanung_xtf/ch.so.arp.nutzungsplanung.xtf
```

## GRETL
```
export ORG_GRADLE_PROJECT_dbUriPub=jdbc:postgresql://localhost:54322/pub
export ORG_GRADLE_PROJECT_dbUserPub=admin
export ORG_GRADLE_PROJECT_dbPwdPub=admin
```

Viele doppelte Stützpunkte, die m.E. auf Fehler in den Ursprungsdaten zurückzuführen sind: Löcher in der AREA, die eigentlich nicht gewollt sind.