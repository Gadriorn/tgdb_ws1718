# Tutorium - Grundlagen Datenbanken - Blatt 2

## Vorbereitungen
* Für dieses Aufgabenblatt wird die SQL-Dump-Datei `tutorium.sql` benötigt, die sich im Verzeichnis `sql` befindet.
* Die SQL-Dump-Datei wird in SQL-Plus mittels `start <Dateipfad/zur/sql-dump-datei.sql>` in die Datenbank importiert.
* Beispiele
  * Linux `start ~/Tutorium.sql`
  * Windows `start C:\Users\max.mustermann\Desktop\Tutorium.sql`

## Datenbankmodell
![Datenbankmodell](./img/datamodler_schema.png)

## Aufgaben

### Aufgabe 1
Schaue dir das Datenbankmodell an. Wofür steht hinter dem Datentyp `NUMBER` die Zahlen in den runden Klammern?
Nehme dir die Oracle [Dokumentation](https://docs.oracle.com/cd/B28359_01/server.111/b28318/datatype.htm#CNCPT012) zu Hilfe.

#### Lösung
Für die max länge der Zahlenkombination.

### Aufgabe 2
Was bedeuten die durchgezogenen Linien, die zwischen einigen Tabellen abgebildet sind?

#### Lösung
Einen verweis des zusammenhangs der beiden Tabellen

### Aufgabe 3
Was bedeutet die gestrichelte Linie, die zwischen der Tabelle `ACC_VEHIC` und `GAS_STATION` abgebildet ist?

#### Lösung
Deine schriftliche Antwort.

### Aufgabe 4
Die folgende Abbildung beschreibt eine Beziehung zwischen Tabellen. Sie wird auch `n` zu `m` Beziehung genannt. Beschreibe kurz die Bedeutung dieser Beziehung.
Nehme dir diesen [Artikel](https://glossar.hs-augsburg.de/Beziehungstypen) zu Hilfe.

![n-to-m-relationship](./img/n-to-m-relationship.png)

Eine n zu m beziehung bedeutet das ein datensatz aus einer Tabelle mehreren Datensätzen einer anderen Tabelle zugeordnet werden kann. Dies gilt auch umgekehrt.

### Aufgabe 5
Was bedeutet der Buchstabe `P` und `F` neben den Attributen von Tabellen?

#### Lösung
P steht für Primärschlüssel und F für Fremdschlüssel

### Aufgabe 6
Importiere die SQL-Dump-Datei in dein eigenes Schema. Wie lautet dazu der Befehl um dem import zu starten?

#### Lösung
start (dateipfad)

### Aufgabe 7
Gebe alle Datensätze der Tabelle `ACCOUNT` aus.

#### Lösung
select *
from Account;

### Aufgabe 8
Modifiziere Aufgabe 7 so, dass nur die Spalte `ACCOUNT_ID` ausgegeben wird.

#### Lösung
select ACCOUNT_ID
from ACCOUNT;

### Aufgabe 9
Gebe alle Spalten der Tabelle `VEHICLE` aus.

#### Lösung
select*
from VEHICLE;

### Aufgabe 10
Kombiniere Aufgabe 7 und 9 so, dass nur Personen (`ACCOUNT`) angezeigt werden, die ein Auto (`VEHICLE`) besitzen.

#### Lösung
SELECT DISTINCT account.* 
FROM ACCOUNT account, ACC_VEHIC vehicle 
WHERE account.ACCOUNT_ID = vehicle.ACCOUNT_ID;

### Aufgabe 11
Modifizierde die Aufgabe 10 so, dass nur die Person mit der `ACCOUNT_ID` = `7` angezeigt wird.

#### Lösung
SELECT DISTINCT account.* 
FROM ACCOUNT account, ACC_VEHIC vehicle 
WHERE account.ACCOUNT_ID = vehicle.ACCOUNT_ID
AND vehicle.ACCOUNT_ID =7;

### Aufgabe 12
Erstelle für dich einen neuen Benutzer.
> Achtung, nutze für die Spalten `C_DATE` und `U_DATE` vorerst die Syntax `SYSDATE` - [Dokumentation](https://docs.oracle.com/cd/B19306_01/server.102/b14200/functions172.htm)

#### Lösung
INSERT into ACCOUNT
VALUES ('10', 'Nils', 'Lemm', 'lemmn@hochschule-trier.de', sysdate, sysdate);

### Aufgabe 13
Erstelle für deinen neuen Benutzer ein neues Auto. Dieses Auto dient als Vorlage für die nächten Aufgaben.

#### Lösung
INSERT into VEHICLE
VALUES ((SELECT MAX(VEHICLE_ID)+ 1 from Vehicle), 1, 6, 'DIVOLO', 3, 590, '08.11.2017', 2, sysdate, sysdate);

### Aufgabe 14
Verknüpfe das aus Aufgabe 13 erstellte neue Auto mit deinem neuen Benutzer aus Aufgabe 12 in der Tabelle `ACC_VEHIC` und erstelle den ersten Rechnungsbeleg.

#### Lösung
insert into ACC_VEHIC
valus ((Select MAX (ACC_VEHIC_ID) +1 from ACC_VEHIC), 
10, 
14,
 'Ferrari Diabolo',
 'Ferrari', 
 null, 
 null, 
 400000,
 150,
 null, 
 '12.12.2017',
 null,
 sysdate, 
 sysdate );
```

### Aufgabe 15
Ändere den Vorname `SURNAME` des Datensatzes mit der ID `7` in der Tabelle `ACCOUNT` auf `Zimmermann`.

#### Lösung
update ACCOUNT
set Surname = 'Zimmerman' where ACCOUNT_ID= '7';
```

### Aufgabe 16
Speichere alle Änderungen deiner offenen Transaktion. Wie lautet der SQL-Befehl dazu?

#### Lösung
commit
```
