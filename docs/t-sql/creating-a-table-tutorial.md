---
title: "Erstellen einer Tabelle (Lernprogramm) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Erstellen von Tabellen"
ms.assetid: 653f2dd3-36a2-4bd5-8703-71a57d244661
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Erstellen einer Tabelle (Lernprogramm)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

Zum Erstellen einer Tabelle müssen Sie einen Tabellennamen sowie die Namen und Datentypen jeder Spalte in der Tabelle angeben. Außerdem empfiehlt es sich, anzugeben, ob NULL-Werte in den einzelnen Spalten zulässig sind. Zum Erstellen der Tabelle müssen Sie über die Berechtigung `CREATE TABLE` verfügen sowie über die Berechtigung `ALTER SCHEMA` für das Schema, das die Tabelle enthalten wird. Die feste Datenbankrolle `db_ddladmin` verfügt über folgende Berechtigungen.  
  
Die meisten Tabellen verfügen über einen Primärschlüssel, der sich aus einer oder mehreren Spalten der Tabelle zusammensetzt. Ein Primärschlüssel ist immer eindeutig. [!INCLUDE[ssDE](../includes/ssde-md.md)] erzwingt die Einschränkung, dass ein Primärschlüsselwert in der Tabelle nicht wiederholt werden kann.  
  
Eine Liste der Datentypen sowie Links zu Beschreibungen der einzelnen Datentypen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md).  
  
> [!NOTE]  
> [!INCLUDE[ssDE](../includes/ssde-md.md)] kann mit oder ohne Beachtung der Groß-/Kleinschreibung installiert werden. Wurde [!INCLUDE[ssDE](../includes/ssde-md.md)] so installiert, dass die Groß-/Kleinschreibung beachtet wird, müssen Objektnamen immer die gleiche Groß-/Kleinschreibung aufweisen. Beispielsweise unterscheidet sich eine Tabelle namens OrderData von einer Tabelle namens ORDERDATA. Wurde [!INCLUDE[ssDE](../includes/ssde-md.md)] so installiert, dass die Groß-/Kleinschreibung nicht beachtet wird, bezeichnen diese beiden Tabellennamen die gleiche Tabelle, und der Name kann nur einmal verwendet werden.  
  
### So erstellen Sie eine Datenbank, die eine neue Tabelle enthält  
  
-   Geben Sie den folgenden Code in ein Abfrage-Editor-Fenster ein.  
  
    ```  
    USE master;  
    GO  
  
    --Delete the TestData database if it exists.  
    IF EXISTS(SELECT * from sys.databases WHERE name='TestData')  
    BEGIN  
        DROP DATABASE TestData;  
    END  
  
    --Create a new database called TestData.  
    CREATE DATABASE TestData;  
    Press the F5 key to execute the code and create the database.  
    ```  
  
### Ändern der Verbindung des Abfrage-Editors in die Datenbank TestData  
  
-   Geben Sie in einem Abfrage-Editorfenster den folgenden Code ein, und führen Sie ihn aus, um die Verbindung in die `TestData` -Datenbank zu ändern.  
  
    ```  
    USE TestData  
    GO  
    ```  
  
### So erstellen Sie eine Tabelle  
  
-   Geben Sie in einem Abfrage-Editorfenster den folgenden Code ein, und führen Sie ihn aus, um eine einfache Tabelle namens `Products`zu erstellen. Die Spalten in der Tabelle heißen `ProductID`, `ProductName`, `Price`und `ProductDescription`. Die `ProductID` -Spalte ist der Primärschlüssel der Tabelle. `int`, `varchar(25)`, `money`und `text` sind Datentypen. Nur die Spalten `Price` und `ProductionDescription` dürfen keine Daten enthalten, wenn eine Zeile eingefügt oder geändert wird. Diese Anweisung enthält ein optionales Element (`dbo.`), das als Schema bezeichnet wird. Das Schema ist das Datenbankobjekt, das die Tabelle besitzt. Wenn Sie Administrator sind, ist `dbo` das Standardschema. `dbo` steht für Datenbankbesitzer (database owner, dbo).  
  
    ```  
    CREATE TABLE dbo.Products  
       (ProductID int PRIMARY KEY NOT NULL,  
        ProductName varchar(25) NOT NULL,  
        Price money NULL,  
        ProductDescription text NULL)  
    GO  
    ```  
  
## Nächste Aufgabe in der Lektion  
[Einfügen und Aktualisieren von Daten in einer Tabelle &#40;Tutorial&#41;](../t-sql/inserting-and-updating-data-in-a-table-tutorial.md)  
  
## Siehe auch  
[CREATE TABLE &#40;Transact-SQL&#41;](../t-sql/statements/create-table-transact-sql.md)  
  
  
  
