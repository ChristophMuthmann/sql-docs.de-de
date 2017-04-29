---
title: "Angeben des Füllfaktors für einen Index | Microsoft-Dokumentation"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- fill factor [SQL Server]
- page splits [SQL Server]
ms.assetid: 237a577e-b42b-4adb-90cf-aa7fb174f3ab
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 60356d04463b7905e092ddb8ccc6374fe410719b
ms.lasthandoff: 04/11/2017

---
# <a name="specify-fill-factor-for-an-index"></a>Angeben des Füllfaktors für einen Index
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, was ein Füllfaktor ist und wie ein Füllfaktorwert in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] für einen Index mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]angegeben wird.  
  
 Die Füllfaktoroption wird zur erweiterten Leistungsoptimierung beim Speichern von Indexdaten bereitgestellt. Wenn ein Index erstellt oder neu erstellt wird, bestimmt der Füllfaktorwert den prozentualen Speicherplatz, der auf jeder Blattebenenseite mit Daten gefüllt werden soll. Der Rest jeder Seite wird als freier Speicherplatz für zukünftige Erweiterungen reserviert. Wenn Sie beispielsweise einen Füllfaktorwert von 80 angeben, bedeutet dies, dass 20 Prozent jeder Seite auf der Blattebene leer gelassen werden, um Speicherplatz für zukünftige Indexerweiterungen bereitzustellen, während der zugrunde liegenden Tabelle Daten hinzugefügt werden. Der freie Speicherplatz wird zwischen den Indexzeilen statt am Ende des Indexes reserviert.  
  
 Der Wert des Füllfaktors ist ein Prozentwert von 1 bis 100, und der serverweite Standardwert ist 0, d. h., dass die Seiten auf Blattebene vollständig aufgefüllt werden.  
  
> [!NOTE]  
>  Die Füllfaktorwerte 0 und 100 sind in jeder Hinsicht identisch.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Leistungsaspekte](#Performance)  
  
     [Sicherheit](#Security)  
  
-   **So geben Sie einen Füllfaktor für einen Index an mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Performance"></a> Leistungsaspekte  
  
#### <a name="page-splits"></a>Seitenteilung  
 Mit einem richtig ausgewählten Füllfaktor kann das Risiko von Seitenteilungen verringert werden, indem genug Speicherplatz für Indexerweiterungen bereitgestellt wird, während der dem Index zugrunde liegenden Tabelle Daten hinzugefügt werden. Wenn einer vollen Indexseite eine neue Zeile hinzugefügt wird, verschiebt [!INCLUDE[ssDE](../../includes/ssde-md.md)] ungefähr die Hälfte der Zeilen auf eine neue Seite, um Platz für die neue Zeile bereitzustellen. Diese Neuorganisation wird auch Seitenteilung genannt. Eine Seitenteilung schafft Platz für neue Datensätze, beansprucht jedoch Zeit und Ressourcen. Seitenteilungen können auch Fragmentierungen verursachen, die zu vermehrten E/A-Vorgängen führen. Bei häufigen Seitenteilungen kann der Index neu erstellt und dabei ein neuer oder bereits vorhandener Füllfaktor verwendet werden, um die Daten neu zu verteilen. Weitere Informationen finden Sie unter [Neuorganisieren und Neuerstellen von Indizes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
 Ein niedriger Füllfaktor über 0 kann zwar beim Vergrößern des Indexes die Seitenteilung reduzieren; der Index erfordert dann jedoch mehr Speicherplatz, was die Leseleistung verringern kann. Sogar im Fall einer Anwendung, die sehr viele Einfügungen und Aktualisierungen vornimmt, treten Datenbanklesevorgänge in der Regel fünf- bis zehnmal häufiger auf als Schreibvorgänge in der Datenbank. Aus diesem Grund kann das Ändern des Standardfüllfaktors die Leistung von Datenbanklesevorgängen in einem Umfang mindern, der umgekehrt proportional zur Füllfaktoreinstellung ist. Ein Füllfaktorwert von 50 Prozent kann z. B. dazu führen, dass die Dauer von Datenbanklesevorgängen verdoppelt wird. Die Leseleistung verringert sich, weil der Index eine größere Anzahl an Seiten enthält und daher die zum Abrufen der Daten erforderlichen Datenträger-E/A-Vorgänge zunehmen.  
  
#### <a name="adding-data-to-the-end-of-the-table"></a>Hinzufügen von Daten zum Tabellenende  
 Ein Füllfaktor ungleich 0 oder 100 kann zur Leistungsverbesserung beitragen, wenn die neuen Daten gleichmäßig in der Tabelle verteilt werden. Wenn jedoch alle Daten am Tabellenende hinzugefügt werden, wird der freie Speicherplatz auf den Indexseiten nicht aufgefüllt. Wenn die Indexschlüsselspalte z. B. eine IDENTITY-Spalte ist, wird der Schlüssel für neue Zeilen stets erhöht, und die Indexzeilen werden am Ende des Indexes logisch hinzugefügt. Wenn vorhandene Zeilen mit Daten aktualisiert werden, die die Größe der Zeilen verlängern, verwenden Sie einen Füllfaktor von weniger als 100. Durch die zusätzlichen Bytes auf jeder Seite werden die Seitenteilungen minimiert, die durch die zusätzliche Länge der Zeilen verursach werden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung in der Tabelle oder Sicht. Der Benutzer muss ein Mitglied der festen Serverrolle **sysadmin** bzw. der festen Datenbankrollen **db_ddladmin** und **db_owner** sein.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-specify-a-fill-factor-by-using-table-designer"></a>So geben Sie einen Füllfaktor mit dem Tabellen-Designer an  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um die Datenbank mit der Tabelle zu erweitern, für die Sie den Füllfaktor eines Indexes angeben möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Tabelle, für die Sie den Füllfaktor eines Indexes angeben möchten, und wählen Sie die Option **Entwurf**.  
  
4.  Klicken Sie im Menü **Tabellen-Designer** auf **Indizes/Schlüssel**.  
  
5.  Wählen Sie den Index mit dem Füllfaktor aus, den Sie angeben möchten.  
  
6.  Erweitern Sie **Füllspezifikation**, wählen Sie die Zeile **Füllfaktor** aus, und geben Sie den gewünschten Füllfaktor in die Zeile ein.  
  
7.  Klicken Sie auf **Schließen**.  
  
8.  Klicken Sie im Menü **Datei** auf **Speichern***table_name*.  
  
#### <a name="to-specify-a-fill-factor-in-an-index-by-using-object-explorer"></a>So geben Sie einen Füllfaktor in einem Index mit dem Objekt-Explorer an  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um die Datenbank mit der Tabelle zu erweitern, für die Sie den Füllfaktor eines Indexes angeben möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, für die Sie den Füllfaktor eines Indexes angeben möchten.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Indizes** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf den Index mit dem Füllfaktor, den Sie angeben möchten, und wählen Sie **Eigenschaften**.  
  
6.  Wählen Sie unter **Seite auswählen**die Option **Optionen**aus.  
  
7.  Geben Sie in der Zeile **Füllfaktor** den gewünschten Füllfaktor ein.  
  
8.  Klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-specify-a-fill-factor-in-an-existing-index"></a>So geben Sie einen Füllfaktor für einen vorhandenen Index an  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Im folgenden Beispiel wird ein vorhandener Index neu erstellt und der angegebene Füllfaktor während der Neuerstellung angewendet.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Rebuilds the IX_Employee_OrganizationLevel_OrganizationNode index   
    -- with a fill factor of 80 on the HumanResources.Employee table.  
  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    REBUILD WITH (FILLFACTOR = 80);   
    GO  
    ```  
  
#### <a name="another-way-to-specify-a-fill-factor-in-an-index"></a>Alternative Möglichkeit zum Angeben eines Füllfaktors in einem Index  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    /* Drops and re-creates the IX_Employee_OrganizationLevel_OrganizationNode index on the HumanResources.Employee table with a fill factor of 80.  
    */  
  
    CREATE INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
       (OrganizationLevel, OrganizationNode)   
    WITH (DROP_EXISTING = ON, FILLFACTOR = 80);   
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
  

