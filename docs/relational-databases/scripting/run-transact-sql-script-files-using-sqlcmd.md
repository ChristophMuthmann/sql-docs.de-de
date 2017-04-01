---
title: "Ausf&#252;hren von Transact-SQL-Skriptdateien mithilfe von sqlcmd | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Transact-SQL-Skripts"
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
caps.latest.revision: 42
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Ausf&#252;hren von Transact-SQL-Skriptdateien mithilfe von sqlcmd
 Verwenden Sie zum Ausführen einer Transact-SQL-Skriptdatei den Befehl **sqlcmd**. Eine Transact-SQL-Skriptdatei ist eine Textdatei, die eine Kombination aus Transact-SQL-Anweisungen, **sqlcmd**-Befehlen und Skriptvariablen enthalten kann.  

## Erstellen einer Skriptdatei  
 Führen Sie die folgenden Schritte aus, um eine einfache Transact-SQL-Skriptdatei mithilfe des Editors zu erstellen:  
  
1.  Klicken Sie auf **Start**, zeigen Sie auf **Alle Programme**, zeigen Sie auf **Zubehör**, und klicken Sie dann auf **Editor**.  
  
2.  Kopieren Sie den folgenden Transact-SQL-Code, und fügen Sie ihn im Editor ein:  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT p.FirstName + ' ' + p.LastName AS 'Employee Name',  
    a.AddressLine1, a.AddressLine2 , a.City, a.PostalCode   
    FROM Person.Person AS p   
       INNER JOIN HumanResources.Employee AS e   
            ON p.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.BusinessEntityAddress bea   
            ON bea.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.Address AS a   
            ON a.AddressID = bea.AddressID;  
    GO  
    ```  
  
3.  Speichern Sie die Datei auf dem Laufwerk C unter dem Namen **myScript.sql** .  
  
## Ausführen der Skriptdatei  
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster.  
  
2.  Geben Sie im Eingabeaufforderungsfenster Folgendes ein: **sqlcmd -S myServer\instanceName -i C:\myScript.sql**  
  
3.  Drücken Sie die EINGABETASTE.  
  
 Eine Liste mit Namen und Adressen von Mitarbeitern aus [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] wird in das Eingabeaufforderungsfenster geschrieben.  

## Speichern der Ausgabe in einer Textdatei
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster.  
  
2.  Geben Sie im Eingabeaufforderungsfenster Folgendes ein: **sqlcmd -S myServer\instanceName -i C:\myScript.sql -o C:\EmpAdds.txt**  
  
3.  Drücken Sie die EINGABETASTE.  
  
 In diesem Fall erfolgt keine Ausgabe im Eingabeaufforderungsfenster. Stattdessen erfolgt die Ausgabe in die Datei EmpAdds.txt. Sie können diese Ausgabe prüfen, indem Sie die Datei EmpAdds.txt öffnen.  
  
## Siehe auch  
 [Starten des Hilfsprogramms "sqlcmd"](../../relational-databases/scripting/start-the-sqlcmd-utility.md)   
 [sqlcmd (Hilfsprogramm)](../../tools/sqlcmd-utility.md)  
  
  