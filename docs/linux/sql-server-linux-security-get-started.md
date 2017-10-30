---
title: Erste Schritte mit SQL Server-Sicherheit unter Linux | Microsoft Docs
description: Dieses Thema beschreibt die typischen Sicherheitsaktionen.
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.custom: H1Hack27Feb2017
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 254df7047188570cbf766efb29b486d77d095a98
ms.contentlocale: de-de
ms.lasthandoff: 10/02/2017

---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Exemplarische Vorgehensweise für die Sicherheitsfeatures von SQL Server on Linux

Wenn Sie einen Linux-Benutzer, der noch nicht mit SQL Server ist sind, führen die folgenden Aufgaben durch einige der Sicherheitsaufgaben. Diese sind nicht eindeutig oder gelten speziell für Linux, aber sie hilft bei der bieten einen Überblick über Bereiche genauere Untersuchung durchführen. In jedem Beispiel wird ein Link, um die ausführliche Dokumentation für diesen Bereich bereitgestellt.

>  [!NOTE]
>  Die folgenden Beispiele verwenden die **"adventureworks2014"** -Beispieldatenbank. Informationen zum Herunterladen und Installieren dieser Beispieldatenbank finden Sie unter [wiederherstellen eine SQL Server-Datenbank von Windows, Linux](sql-server-linux-migrate-restore-database.md).


## <a name="create-a-login-and-a-database-user"></a>Erstellen Sie eine Anmeldung und einen Datenbankbenutzer 

Gewähren Sie andere Benutzer Zugriff auf SQL Server durch Erstellen eines Anmeldenamens in der master-Datenbank mithilfe der [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) Anweisung. Beispiel:

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

>  [!NOTE]
>  Verwenden Sie immer ein sicheres Kennwort anstelle der oben genannten Sternchen.

Anmeldungen können eine Verbindung mit SQL Server und Zugriffsrechte (mit eingeschränkten Berechtigungen) für die master-Datenbank. Zur Verbindung mit einer Benutzerdatenbank benötigt eine Anmeldung eine entsprechende Identität auf Datenbankebene, einen Datenbankbenutzer bezeichnet. Benutzer sind für jede Datenbank spezifisch und müssen separat erstellt werden, in jeder Datenbank aus, um ihnen den Zugriff zu erteilen. Im folgende Beispiel wird Sie in der AdventureWorks2014-Datenbank verschoben und verwendet dann die [CREATE USER](../t-sql/statements/create-user-transact-sql.md) -Anweisung zum Erstellen einer Benutzers namens Larry, die mit der Anmeldung mit dem Namen Larry anfallen. Obwohl die Anmeldung und der Benutzer verknüpft sind (die miteinander verknüpft sind), handelt es sich um unterschiedliche Objekte. Der Anmeldename ist einem Prinzipal auf Serverebene. Der Benutzer ist ein Prinzipal auf Datenbankebene.

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- Ein SQL Server-Administratorkonto auf eine beliebige Datenbank herstellen kann und weitere Anmeldungen und Benutzer kann in jeder Datenbank erstellen.  
- Wenn ein Benutzer eine Datenbank erstellt wird, werden sie Besitzer der Datenbank, eine Verbindung zu dieser Datenbank herstellen kann. Datenbankbesitzer können weitere Benutzer erstellen.

Später können Sie andere Anmeldenamen eine weitere Anmeldungen zu erstellen, indem Sie erteilen diese Autorisieren der `ALTER ANY LOGIN` Berechtigung. Innerhalb einer Datenbank, autorisieren Sie anderen Benutzern an weitere Benutzer zu erstellen, indem sie erteilen der `ALTER ANY USER` Berechtigung. Beispiel:   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

Jetzt die Anmeldung Jerry können weitere Anmeldungen erstellen, und der Benutzer Jerry kann weitere Benutzer erstellen.


## <a name="granting-access-with-least-privileges"></a>Erteilen des Zugriffs mit den geringsten Privilegien

Die erste Personen für die Verbindung mit einer Benutzerdatenbank werden das Administrator- und Konten für Datenbank-Besitzer. Jedoch diese Benutzer verfügen alle über die Berechtigungen für die Datenbank verfügbar. Dies ist über mehr Berechtigungen verfügen als die meisten Benutzer haben sollen. 

Wenn Sie nur noch am Anfang stehen, können Sie einige allgemeine Kategorien von Berechtigungen zuweisen, mithilfe der integriertes *festen Datenbankrollen*. Z. B. die `db_datareader` festen Datenbankrolle "" alle Tabellen in der Datenbank lesen kann, aber keine Änderungen vornehmen. Mitgliedschaft in einer festen Datenbankrolle zu gewähren, mithilfe der [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md) Anweisung. Im folgende Beispiel fügen Sie den Benutzer `Jerry` auf die `db_datareader` festen Datenbankrolle "".   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

Eine Liste der festen Datenbankrollen, finden Sie unter [Datenbankrollen](../relational-databases/security/authentication-access/database-level-roles.md).

Später, wenn Sie eine genauere den Zugriff auf Ihre Daten (empfohlen) konfigurieren möchten, erstellen eine eigene benutzerdefinierte Datenbankrollen, die mit [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md) Anweisung. Sie benutzerdefinierte Rollen bestimmte präzise Berechtigungen zuweisen.

Z. B. die folgenden Anweisungen erstellen eine Datenbankrolle mit dem Namen `Sales`, gewährt die `Sales` gruppieren Sie die Möglichkeit, finden Sie unter, aktualisieren und Löschen von Zeilen aus der `Orders` Tabelle, und fügt dann den Benutzer `Jerry` auf die `Sales` Rolle.   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```   

Weitere Informationen über das Berechtigungssystem finden Sie unter [erste Schritte mit Berechtigungen für das Datenbankmodul](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).


## <a name="configure-row-level-security"></a>Konfigurieren der Sicherheit auf Zeilenebene  

[Sicherheit auf Zeilenebene](../relational-databases/security/row-level-security.md) ermöglicht es Ihnen, den Zugriff auf die Zeilen in einer Datenbank, basierend auf dem Benutzer, die Ausführung einer Abfrage einschränken. Diese Funktion eignet sich für Szenarien wie das sicherstellen, dass Kunden nur ihre eigenen Daten zugreifen können, oder dass Mitarbeiter nur auf Daten zugreifen können, die für ihre Abteilung relevant ist.   

Die Schritte unten Gang durch das Einrichten von zwei Benutzern mit verschiedenen Zeilenebene Zugriff auf die `Sales.SalesOrderHeader` Tabelle. 

Erstellen Sie zwei Benutzerkonten zum Testen der Sicherheit auf Zeilenebene:    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

Gewähren Sie Lesezugriff auf die `Sales.SalesOrderHeader` Tabelle für beide Benutzer:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
Erstellen Sie eine neue Schema und Inline-Tabellenwertfunktion. Die Funktion gibt 1, wenn eine Zeile in der `SalesPersonID` Spalte entspricht die ID des eine `SalesPerson` Anmeldung oder wenn der Benutzer, die Ausführung der Abfrage der ManagerBenutzer ist.   
   
```     
CREATE SCHEMA Security;   
GO   
   
CREATE FUNCTION Security.fn_securitypredicate(@SalesPersonID AS int)     
    RETURNS TABLE   
WITH SCHEMABINDING   
AS     
   RETURN SELECT 1 AS fn_securitypredicate_result    
WHERE ('SalesPerson' + CAST(@SalesPersonId as VARCHAR(16)) = USER_NAME())     
    OR (USER_NAME() = 'Manager');    
```   

Erstellen Sie eine Sicherheitsrichtlinie, die die Funktion als eine Filter- und Block-Prädikat für die Tabelle hinzufügt:  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

Führen Sie die folgende Abfrage die `SalesOrderHeader` Tabelle als jeweiliger Benutzer. Überprüfen Sie, ob `SalesPerson280` sieht nur ihre eigenen Verkäufe und dass 95 Zeilen der `Manager` sehen, dass alle Zeilen in der Tabelle.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
Ändern Sie die Sicherheitsrichtlinie, um die Richtlinie zu deaktivieren.  Jetzt können sowohl Benutzer alle Zeilen zugreifen. 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## <a name="enable-dynamic-data-masking"></a>Aktivieren Sie die dynamische datenmaskierung

[Dynamische Datenmaskierung](../relational-databases/security/dynamic-data-masking.md) ermöglicht es Ihnen, die Offenlegung sensibler Daten für Benutzer einer Anwendung von vollständig oder teilweise maskieren bestimmte Spalten beschränken. 

Verwenden einer `ALTER TABLE` -Anweisung eine Maskierungsfunktion zum Hinzufügen der `EmailAddress` Spalte in der `Person.EmailAddress` Tabelle: 
 
```
USE AdventureWorks2014;
GO
ALTER TABLE Person.EmailAddress    
ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
Erstellen eines neuen Benutzers `TestUser` mit `SELECT` Berechtigung für die Tabelle, führen Sie dann eine Abfrage als `TestUser` zum Anzeigen der maskierten Daten:   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
Stellen Sie sicher, dass der Maskierungsfunktion ändert, die e-Mail-Adresse des ersten Datensatzes aus:
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## <a name="enable-transparent-data-encryption"></a>Aktivieren der transparenten Datenverschlüsselung

Eine Bedrohung für Ihre Datenbank ist das Risiko, dass ein Benutzer die Datenbankdateien aus der Festplatte stehlen wird. Dies kann auf einen Eindringversuch passieren, die mit erhöhten Rechten Zugriff auf das System über die Aktionen eines Mitarbeiters Problem oder durch den Diebstahl von dem Computer mit den Dateien (z. B. einen Laptop) abruft.

Transparente datenverschlüsselung (TDE) verschlüsselt die Datendateien aus, sobald sie auf der Festplatte gespeichert werden. Der master-Datenbank des Datenbankmoduls von SQL Server hat den Verschlüsselungsschlüssel, damit das Datenbankmodul die Daten bearbeiten kann. Die Datenbankdateien nicht ohne Zugriff auf den Schlüssel nicht gelesen werden. Allgemeine Administratoren können verwalten, Sicherung, und den Schlüssel neu erstellen, damit die Datenbank verschoben werden kann, sondern nur vom ausgewählten Personen. Wenn TDE konfiguriert ist, die `tempdb` Datenbank ebenfalls automatisch verschlüsselt. 

Da das Datenbankmodul die Daten lesen kann, wird Transparent Data Encryption nicht vor nicht autorisiertem Zugriff, die Administratoren von dem Computer zu schützen, können direkt Speicher gelesen oder Zugriff auf SQL Server über ein Administratorkonto.

### <a name="configure-tde"></a>Konfigurieren von TDE

- Erstellen Sie einen Hauptschlüssel
- Erstellen oder beziehen Sie ein vom Hauptschlüssel geschütztes Zertifikat
- Erstellen Sie einen Verschlüsselungsschlüssel für die Datenbank, und schützen Sie ihn durch das Zertifikat
- Legen Sie fest, dass für die Datenbank Verschlüsselung verwendet wird

Konfigurieren von TDE erfordert `CONTROL` -Berechtigung für die master-Datenbank und `CONTROL` -Berechtigung für die Benutzerdatenbank. In der Regel konfiguriert ein Administrator TDE. 

Im folgenden Beispiel wird die Verschlüsselung und Entschlüsselung der `AdventureWorks2014` -Datenbank gezeigt, wobei ein auf dem Server `MyServerCert`installiertes Zertifikat verwendet wird.


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
GO  

USE AdventureWorks2014;  
GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON;   
```

Um TDE zu entfernen, führen`ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

Die Verschlüsselung und Entschlüsselung Vorgänge werden von SQL Server in Hintergrundthreads geplant. Sie können den Status dieser Vorgänge mithilfe der in der Liste weiter unten in diesem Thema genannten Katalogsichten und dynamischen Verwaltungssichten anzeigen.   

>  [!WARNING]
>  Sicherungsdateien von Datenbanken, für die TDE aktiviert wurde, werden ebenfalls mithilfe des Verschlüsselungsschlüssels für die Datenbank verschlüsselt. Darum muss bei der Wiederherstellung dieser Sicherungen das Zertifikat, das zum Verschlüsseln des Verschlüsselungsschlüssels für die Datenbank verwendet wurde, verfügbar sein. Dies bedeutet, dass Sie zusätzlich zur Sicherung der Datenbank auch Sicherungskopien der Serverzertifikate aufbewahren müssen, um einem Datenverlust vorzubeugen. Ist das Zertifikat nicht mehr verfügbar, kann es zu einem Datenverlust kommen. Weitere Informationen finden Sie unter [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  

Weitere Informationen zu TDE finden Sie unter [transparente datenverschlüsselung (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md).   


## <a name="configure-backup-encryption"></a>Konfigurieren von sicherungsverschlüsselung
SQL Server hat die Möglichkeit zum Verschlüsseln der Daten beim Erstellen einer Sicherung. Durch Angeben des Verschlüsselungsalgorithmus und der Verschlüsselung (ein Zertifikat oder asymmetrischen Schlüssel) beim Erstellen einer Sicherung können Sie eine verschlüsselte Sicherungsdatei anlegen.    
  
> [!WARNING]  
>  Es ist sehr wichtig, das Zertifikat oder den asymmetrischen Schlüssel zu sichern – vorzugsweise an einem anderen Speicherort als die Sicherungsdatei, die zum Verschlüsseln verwendet wurde. Ohne das Zertifikat oder den asymmetrischen Schlüssel können Sie keine Sicherung wiederherstellen, sodass die Sicherungsdatei unbrauchbar ist. 
 
 
Im folgenden Beispiel wird ein Zertifikat erstellt, und erstellt dann eine Sicherung, die durch das Zertifikat geschützt.
```
USE master;  
GO  
CREATE CERTIFICATE BackupEncryptCert   
   WITH SUBJECT = 'Database backups';  
GO 
BACKUP DATABASE [AdventureWorks2014]  
TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```

Weitere Informationen finden Sie unter [Sicherungsverschlüsselung](../relational-databases/backup-restore/backup-encryption.md).


## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu den Sicherheitsfeatures von SQL Server finden Sie unter [Sicherheitscenter für SQL Server-Datenbankmodul und Azure SQL-Datenbank](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

